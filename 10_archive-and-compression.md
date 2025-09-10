# 10. アーカイブと圧縮

Linux でファイルやディレクトリをまとめたり（アーカイブ）、サイズを小さくする（圧縮）方法を学ぶ。  
主に `tar` コマンドを利用する。

---

## 課題1: tar でアーカイブを作成

### コマンド例
```bash
mkdir archive_test
echo "file1" > archive_test/file1.txt
echo "file2" > archive_test/file2.txt

tar -cvf archive_test.tar archive_test
ls -lh archive_test.tar
```

### 出力例
```
-rw-r--r-- 1 user user 10K ... archive_test.tar
```

- `c` = create（作成）  
- `v` = verbose（処理内容を表示）  
- `f` = file（アーカイブファイル名を指定）  

→ ディレクトリごと `archive_test.tar` にまとめられる。

---

## 課題2: tar アーカイブを展開

### コマンド例
```bash
mkdir extract_test
tar -xvf archive_test.tar -C extract_test
ls -R extract_test
```

### 出力例
```
extract_test/
└── archive_test/
    ├── file1.txt
    └── file2.txt
```

- `x` = extract（展開）  
- `-C ディレクトリ` = 展開先を指定  
- 指定しない場合はカレントディレクトリに展開される  

---

## 課題3: 圧縮付きアーカイブの作成

### gzip 圧縮
```bash
tar -czvf archive_test.tar.gz archive_test
ls -lh archive_test.tar.gz
```
- `z` = gzip 圧縮  
- 出力ファイル: `.tar.gz`

### bzip2 圧縮
```bash
tar -cjvf archive_test.tar.bz2 archive_test
```
- `j` = bzip2 圧縮  
- 出力ファイル: `.tar.bz2`

### xz 圧縮
```bash
tar -cJvf archive_test.tar.xz archive_test
```
- `J` = xz 圧縮  
- 出力ファイル: `.tar.xz`

---

## 課題4: 圧縮ファイルを展開

### gzip 圧縮ファイルの展開
```bash
tar -xzvf archive_test.tar.gz -C extract_test
```

### 出力例
```
extract_test/
└── archive_test/
    ├── file1.txt
    └── file2.txt
```

---

## まとめ

- `tar -cvf` でアーカイブ作成、`tar -xvf` で展開  
- 圧縮オプションを追加することで `.tar.gz` / `.tar.bz2` / `.tar.xz` を作成可能  
- 展開時も対応するオプションを付ける（gzip=z, bzip2=j, xz=J）  
- `-C` オプションで展開先ディレクトリを指定できる  

