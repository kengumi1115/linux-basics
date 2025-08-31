# 01. ファイル操作

Linuxの基本操作（ファイル・ディレクトリの作成、移動、コピー、削除）の練習。

---

## 課題1: ファイル作成
### お題
1. `practice` ディレクトリを作成  
2. その中に `a.txt` と `b.txt` を作成  
3. `ls` で確認  

### コマンド
```bash
mkdir practice
cd practice
touch a.txt b.txt
ls
```

### 実行結果
```
a.txt  b.txt
```

---

## 課題2: ファイル移動・コピー・削除
### お題
1. `b.txt` を `backup.txt` にリネーム  
2. `a.txt` を一つ上のディレクトリへ移動  
3. `backup.txt` をコピーして `copy.txt` を作成  
4. `copy.txt` を削除  

### コマンド
```bash
mv b.txt backup.txt
mv a.txt ../
cp backup.txt copy.txt
rm copy.txt
```

### 実行結果
```
practice/: backup.txt
ホームディレクトリ: a.txt
```

---

## 課題3: ディレクトリ操作
### お題
1. `dir1` を作成  
2. 中に `test.txt` を作成  
3. `dir1` をコピーして `dir2` を作成  
4. `dir2` を削除  

### コマンド
```bash
mkdir dir1
touch dir1/test.txt
cp -r dir1 dir2
rm -r dir2
ls -R
```

### 実行結果
```
.:
backup.txt  dir1

./dir1:
test.txt
```

---

## 課題4: まとめ練習
### お題
1. `project` を作成  
2. 中に `notes.txt` を作成し、さらに `subdir` を作成  
3. `notes.txt` を `subdir` に移動  
4. `notes.txt` をコピーして `copy.txt` を作成  
5. `copy.txt` を削除  
6. `ls -R project` で確認  

### コマンド
```bash
mkdir project
touch project/notes.txt
mkdir project/subdir
mv project/notes.txt project/subdir/
cp project/subdir/notes.txt project/subdir/copy.txt
rm project/subdir/copy.txt
ls -R project
```

### 実行結果
```
project:
subdir

project/subdir:
notes.txt
```
