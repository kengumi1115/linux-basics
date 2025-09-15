# 15. シェルスクリプト基礎

Linux のシェルスクリプト入門で作成したサンプル集。複数のコマンドを自動実行する練習を行う。

---

## 1) hello.sh

### 内容
```bash
#!/bin/bash
echo "Hello, Linux!"
```

### 実行
```bash
chmod +x ~/myscripts/hello.sh
./myscripts/hello.sh
```
**出力例**
```
Hello, Linux!
```

---

## 2) hello_user.sh

### 内容
```bash
#!/bin/bash
USERNAME=$USER
echo "Hello, $USERNAME!"
```

### 実行
```bash
chmod +x ~/myscripts/hello_user.sh
./myscripts/hello_user.sh
```
**出力例**
```
hello, kengumi1115!
```

---

## 3) greet.sh

### 内容
```bash
#!/bin/bash
echo "Hello, $1!"
```
- `$1` = 最初の引数

### 実行
```bash
chmod +x ~/myscripts/greet.sh
./myscripts/greet.sh kengumi
```
**出力例**
```
HELLO, kengumi!
```

---

## 学びのポイント
- `chmod +x` でスクリプトに実行権限を付与
- `$USER` などの環境変数を参照
- 位置パラメータ `$1` で引数を受け取る
