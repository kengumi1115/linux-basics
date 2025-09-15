# 15. Shell Script Basics（シェルスクリプト基礎）

Linux で「複数コマンドをまとめて自動実行」するための基礎を学びます。  
本章では 3 本のスクリプトを作って、変数・引数・実行権限の基本を固めます。

---

## 学習ゴール

- `#!/bin/bash`（シバン）と実行権限の意味を説明できる  
- 環境変数（例: `$USER`）を参照できる  
- 位置パラメータ（`$1`, `$2`, ...）で引数を受け取れる  
- 最低限のトラブルシューティングができる（パス/権限/改行コード）

---

## 前提 / 準備

```bash
# 作業用ディレクトリ
mkdir -p ~/myscripts
cd ~
```

---

## 課題1: `hello.sh`（固定メッセージの表示）

**ファイル作成**

```bash
nano ~/myscripts/hello.sh
```

**内容**

```bash
#!/bin/bash
echo "Hello, Linux!"
```

**実行権限を付与 → 実行**

```bash
chmod +x ~/myscripts/hello.sh
./myscripts/hello.sh
```

**出力例**

```
Hello, Linux!
```

---

## 課題2: `hello_user.sh`（環境変数の利用）

**ファイル作成**

```bash
nano ~/myscripts/hello_user.sh
```

**内容**

```bash
#!/bin/bash
USERNAME=$USER
echo "Hello, $USERNAME!"
```

**実行権限を付与 → 実行**

```bash
chmod +x ~/myscripts/hello_user.sh
./myscripts/hello_user.sh
```

**出力例（実行環境: ユーザー名 `kengumi1115`）**

```
hello, kengumi1115!
```

> ※ 表示の大文字/小文字は `echo` に書いた通りに出ます。

---

## 課題3: `greet.sh`（引数の受け取り）

**ファイル作成**

```bash
nano ~/myscripts/greet.sh
```

**内容**

```bash
#!/bin/bash
echo "Hello, $1!"
```

**実行権限を付与 → 実行（引数付き）**

```bash
chmod +x ~/myscripts/greet.sh
./myscripts/greet.sh kengumi
```

**出力例**

```
HELLO, kengumi!
```

> ※ ここも `echo` の文字列がそのまま反映されます。

---

## まとめて動作確認（ワンライナー）

```bash
~/myscripts/hello.sh && ~/myscripts/hello_user.sh && ~/myscripts/greet.sh kengumi
```

---

## トラブルシューティング

- **パスのタイプミス**  
  例: `~/myscrips/hello.sh`（`t` 抜け）→ 正: `~/myscripts/hello.sh`

- **ホーム表記の誤り**  
  `~myscripts/hello_user.sh` は **誤り**。`~/myscripts/hello_user.sh` が **正解**。

- **実行権限がない**  
  `permission denied` → `chmod +x <script>` を実行。

- **改行コードの問題（Windowsで作成した場合）**  
  `bash^M: bad interpreter` → `sudo apt install dos2unix && dos2unix <script>`

- **相対/絶対パス**  
  `./myscripts/hello.sh` は「今いる場所からの相対パス」。  
  どこからでも実行したいならフルパス（`/home/<user>/myscripts/hello.sh`）か PATH へ追加。

---

## ミニ課題（発展）

1. **引数が無いときにメッセージを出す**  
   ```bash
   #!/bin/bash
   if [ $# -lt 1 ]; then
     echo "Usage: $0 <name>"
     exit 1
   fi
   echo "Hello, $1!"
   ```

2. **デフォルト値を用意する（引数が無ければユーザー名）**  
   ```bash
   #!/bin/bash
   name="${1:-$USER}"
   echo "Hello, $name!"
   ```

3. **複数引数をまとめて表示する**  
   ```bash
   #!/bin/bash
   echo "Args: $@"
   echo "Count: $#"
   ```

---


## 参考メモ

- **シバン (`#!/bin/bash`)**: どのシェルで実行するかを指定します。  
- **実行ビット (`chmod +x`)**: スクリプトを「実行可能」にするフラグです。  
- **位置パラメータ**: `$0`（スクリプト名）, `$1`（最初の引数）, `$#`（引数の数）, `$@`（全引数） など。

