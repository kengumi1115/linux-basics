# 07. パイプとリダイレクト

Linux でコマンドの出力をファイルに保存したり、別のコマンドに渡す仕組みを学ぶ。  
標準出力（stdout）、標準エラー（stderr）、そして /dev/null の使い方がポイント。

---

## 課題1: 標準出力のリダイレクト

### コマンド例
```bash
# 上書き保存
echo "Hello Linux" > hello.txt
cat hello.txt

# 追記保存
echo "追加行" >> hello.txt
cat hello.txt

# ls の結果をファイルに保存
ls -l > list.txt
cat list.txt
```

- `>` : 上書き保存  
- `>>` : 追記保存  

---

## 課題2: 標準エラーのリダイレクト

### コマンド例
```bash
# 存在しないファイルを読み込む → エラー発生
cat nofile.txt

# エラーをファイルに保存
cat nofile.txt 2> error.log
cat error.log

# 成功と失敗を両方まとめて保存
ls -l /root > all.log 2>&1
cat all.log
```

- `2>` : 標準エラーをリダイレクト  
- `2>&1` : 標準エラーを標準出力にまとめる  

---

## 課題3: 標準出力と標準エラーの同時扱い

### コマンド例
```bash
# 成功（fruits.txt）と失敗（/root）をまとめて保存
ls fruits.txt /root > both.log 2>&1
cat both.log
```

出力例:
```
fruits.txt
ls: cannot open directory '/root': Permission denied
```

- 標準出力と標準エラーが同じファイルに入る  

---

## 課題4: tee コマンド

### コマンド例
```bash
# 出力を画面に表示しつつファイルにも保存
ls -l | tee list2.txt
cat list2.txt

# 追記モード
ls -l | tee -a list2.txt
```

- `tee` は **出力を分岐** させるイメージ  
- 画面にも出しつつファイル保存も可能  

---

## 課題5: /dev/null で出力を捨てる

### コマンド例
```bash
# 標準出力を捨てる
ls > /dev/null

# エラーだけ捨てる
ls /root 2> /dev/null

# 標準出力と標準エラーを両方捨てる
ls /root > /dev/null 2>&1
```

- `/dev/null` は **ブラックホール**  
- 出力が全て捨てられる  

---

## /dev/null の用途

1. **エラーを隠す**  
   ```bash
   ls /root 2> /dev/null
   ```

2. **不要な出力を抑える**  
   ```bash
   command > /dev/null
   ```

3. **cron ジョブの静音化**  
   ```bash
   backup.sh > /dev/null 2>&1
   ```

4. **パフォーマンステスト**  
   ```bash
   time command > /dev/null 2>&1
   ```

---

## まとめ

- `>` / `>>` … 標準出力のリダイレクト  
- `2>` … 標準エラーのリダイレクト  
- `2>&1` … 標準エラーを標準出力とまとめる  
- `tee` … 出力を画面＋ファイルに分岐  
- `/dev/null` … 出力を捨てる「ゴミ箱」  


