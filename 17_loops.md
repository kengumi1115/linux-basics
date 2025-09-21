# 17. ループ基礎（for / while / until）

ループ処理を使って繰り返し実行する方法を学びます。  
`for`、`while`、`until` の3つの基本形と、実践的な課題を扱います。

---

## 学習ゴール
- `for` / `while` / `until` の基本構文を理解する
- ファイルやリストをまとめて処理できる
- 標準入力を1行ずつ処理できる

---

## 課題1: forループで挨拶

### コード
```bash
#!/bin/bash
# Usage: ./for-greet.sh

for name in Alice Bob Charlie; do
  echo "Hello, $name!"
done
```

### 実行例
```
Hello, Alice!
Hello, Bob!
Hello, Charlie!
```

---

## 課題2: whileループでカウントダウン

### コード
```bash
#!/bin/bash
# Usage: ./countdown.sh <number>

if [ -z "$1" ]; then
  echo "Usage: $0 <number>"
  exit 1
fi

n=$1

while [ "$n" -gt 0 ]; do
  echo "$n"
  n=$((n - 1))
done

echo "Lift off!"
```

### 実行例
```
5
4
3
2
1
Lift off!
```

---

## 課題3: untilループで条件を満たすまで実行

### コード
```bash
#!/bin/bash
# Usage: ./until-example.sh

count=1

until [ "$count" -gt 3 ]; do
  echo "Loop $count"
  count=$((count + 1))
done
```

### 実行例
```
Loop 1
Loop 2
Loop 3
```

---

## 課題4: forループでファイルをまとめて処理

### コード
```bash
#!/bin/bash
# Usage: ./list-txt.sh

for file in *.txt; do
  if [ -f "$file" ]; then
    echo "Found: $file"
  fi
done
```

### 実行例
```
Found: a.txt
Found: b.txt
Found: sample.txt
```

---

## 課題5: while read でファイルを1行ずつ処理

### コード
```bash
#!/bin/bash
# Usage: ./read-lines.sh <file>

if [ -z "$1" ]; then
  echo "Usage: $0 <file>"
  exit 1
fi

file="$1"

while IFS= read -r line; do
  echo "Line: $line"
done < "$file"
```

### 実行例
```
Line: apple
Line: banana
Line: cherry
```

---

## まとめ
- `for` はリストやファイル群を処理するのに便利
- `while` は条件が真の間ループ
- `until` は条件が偽の間ループ
- `while read` を使えばファイルや標準入力を1行ずつ扱える

---

