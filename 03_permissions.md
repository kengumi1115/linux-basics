# 03. 権限・ユーザー管理

Linuxでのファイル権限やユーザー管理の基本操作（chmod / chown / sudo）の練習。

---

## 課題1: 権限の確認と変更
### お題
1. `secret.txt` を作成  
2. `ls -l` で確認  
3. `chmod 600 secret.txt` を実行  
4. 再度 `ls -l` で確認  

### コマンドと結果
```bash
touch secret.txt
ls -l secret.txt
chmod 600 secret.txt
ls -l secret.txt
```
```
-rw-r--r-- 1 kengumi1115 kengumi1115 0 Sep  1 22:20 secret.txt
-rw------- 1 kengumi1115 kengumi1115 0 Sep  1 22:20 secret.txt
```

---

## 課題2: 実行権限の付与
### お題
1. `hello.sh` を作成し、内容は `echo "Hello Linux"`  
2. `ls -l hello.sh` で確認  
3. `chmod 755 hello.sh` を実行  
4. `./hello.sh` を実行  

### コマンドと結果
```bash
echo 'echo "Hello Linux"' > hello.sh
ls -l hello.sh
chmod 755 hello.sh
ls -l hello.sh
./hello.sh
```
```
-rw-r--r-- 1 kengumi1115 kengumi1115 19 Sep  1 22:27 hello.sh
-rwxr-xr-x 1 kengumi1115 kengumi1115 19 Sep  1 22:27 hello.sh
Hello Linux
```

---

## 課題3: 所有者の変更
### お題
1. `owner.txt` を作成  
2. `ls -l owner.txt` で確認  
3. `sudo chown root:root owner.txt` を実行  
4. 再度 `ls -l` で確認  

### コマンドと結果
```bash
touch owner.txt
ls -l owner.txt
sudo chown root:root owner.txt
ls -l owner.txt
```
```
-rw-r--r-- 1 kengumi1115 kengumi1115 0 Sep  3 21:16 owner.txt
-rw-r--r-- 1 root root 0 Sep  3 21:16 owner.txt
```

---

## 課題4: sudo の効果を体験
### お題
1. root 所有のファイルを作成  
2. 一般ユーザーで書き込み（失敗する）  
3. sudo 付きで書き込み（成功する）  

### コマンドと結果
```bash
touch root_only.txt
sudo chown root:root root_only.txt
echo "test" > root_only.txt   # Permission denied
sudo sh -c 'echo "test" > root_only.txt'
cat root_only.txt
```
```
-bash: root_only.txt: Permission denied
test
```

---

