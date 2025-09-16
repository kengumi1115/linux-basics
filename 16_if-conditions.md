# 16. if文と条件分岐

スクリプト内で「条件によって処理を分ける」ための基本を学びます。  
`if / elif / else / fi`、比較演算子、ファイルテスト、終了ステータスの扱いを押さえます。

---

## 学習ゴール
- `if / elif / else / fi` の基本構造を説明できる
- 数値・文字列・ファイル属性の条件式を書ける
- コマンドの成功/失敗（終了ステータス）で分岐できる
- パラメータ展開 `${var:-default}` でデフォルト値を扱える

---

## 0) 準備
```bash
mkdir -p ~/myscripts
```

---

## 課題1: 数値を判定する `check_number.sh`

### コード
```bash
#!/bin/bash
# Usage: ./check_number.sh <number>

if [ -z "$1" ]; then
  echo "Usage: $0 <number>"
  exit 1
fi

n="$1"

# 数値でなければエラーにする（Bashの [[ ]] の正規表現マッチ）
if ! [[ "$n" =~ ^-?[0-9]+$ ]]; then
  echo "not a number: $n"
  exit 2
fi

if [ "$n" -gt 0 ]; then
  echo "positive"
elif [ "$n" -lt 0 ]; then
  echo "negative"
else
  echo "zero"
fi
```

### 解説
- `-z "$1"`: 引数が空なら使い方を表示して終了
- `[[ "$n" =~ 正規表現 ]]`: 数値かどうかを安全に判定
- `-gt / -lt`: greater/less than（より大きい / より小さい）

### 実行例
```bash
chmod +x ~/myscripts/check_number.sh
~/myscripts/check_number.sh 5      # positive
~/myscripts/check_number.sh -3     # negative
~/myscripts/check_number.sh 0      # zero
```

---

## 課題2: パスを判定する `file-check.sh`

### コード
```bash
#!/bin/bash
# Usage: ./file-check.sh <path>

p="$1"

if [ -z "$p" ]; then
  echo "Usage: $0 <path>"
  exit 1
fi

if [ -d "$p" ]; then
  echo "directory"
elif [ -f "$p" ]; then
  if [ -x "$p" ]; then
    echo "executable file"
  else
    echo "regular file"
  fi
else
  echo "not found"
fi
```

### 解説
- `-d / -f / -x`: ディレクトリ / 通常ファイル / 実行可能 の各テスト
- 分岐の粒度を「存在 → 種別 → 権限」の順で判定

### 実行例
```bash
chmod +x ~/myscripts/file-check.sh
~/myscripts/file-check.sh ~/myscripts            # directory
~/myscripts/file-check.sh ~/myscripts/check_number.sh  # regular file or executable file
~/myscripts/file-check.sh /no/such/path          # not found
```

---

## 課題3: コマンド結果で分岐する `ping-check.sh`

### コード
```bash
#!/bin/bash
# Usage: ./ping-check.sh [host]

host="${1:-8.8.8.8}"   # 引数が無ければ Google DNS を使う

if ping -c 1 -W 1 "$host" > /dev/null 2>&1; then
  echo "reachable: $host"
else
  echo "unreachable: $host"
fi
```

### 解説
- `if コマンド; then ... fi`: コマンド成功（終了コード0）で then 節へ
- `> /dev/null 2>&1`: 標準出力・標準エラーを捨てて静かに判定
- `${1:-8.8.8.8}`: **$1 が空なら 8.8.8.8** を使う（if/else の短縮）

### 実行例
```bash
chmod +x ~/myscripts/ping-check.sh
~/myscripts/ping-check.sh             # reachable: 8.8.8.8
~/myscripts/ping-check.sh example.com # reachable / unreachable
~/myscripts/ping-check.sh foo.local   # unreachable: foo.local
```

---

## 課題4: デフォルト値つき挨拶 `greet2.sh`

### コード
```bash
#!/bin/bash
# Usage: ./greet2.sh [name]

name="${1:-$USER}"   # $1 が無ければ $USER を使う
echo "Hello, $name!"
```

### 解説
- `${1:-$USER}` は実質的に下記 if/else と同義：  
  ```bash
  if [ -n "$1" ]; then name="$1"; else name="$USER"; fi
  ```

### 実行例
```bash
chmod +x ~/myscripts/greet2.sh
~/myscripts/greet2.sh          # Hello, <あなたのユーザー名>!
~/myscripts/greet2.sh Linux    # Hello, Linux!
```

---

## よくあるエラーと対処
- `[: missing ']'`: 角括弧の前後に**スペース**が無い／閉じ忘れ
- `bash^M: bad interpreter`: Windows改行 → `dos2unix script.sh`
- `No such file or directory`: 実行パスの誤り → `~/myscripts/xxx.sh` か `cd ~/myscripts && ./xxx.sh`
- 変数未クォートで分岐が壊れる → 基本は `"${var}"` で囲む

---

