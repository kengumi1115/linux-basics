# 02. ファイル内容確認

Linuxでテキストやログを確認するための基本コマンド（cat / head / tail / less / wc / grep / tail -f）の練習。

---

## 課題1: ファイル内容を表示する
### お題
1. `sample.txt` を作成し、以下の内容を入れる  
   ```
   line1
   line2
   line3
   ```
2. `cat sample.txt` で全体を表示  
3. `head -n 2 sample.txt` で先頭2行を表示  
4. `tail -n 2 sample.txt` で末尾2行を表示  

### コマンドと実行結果
```bash
echo -e "line1\nline2\nline3" > sample.txt
cat sample.txt
head -n 2 sample.txt
tail -n 2 sample.txt
```
```
line1
line2
line3
line1
line2
line2
line3
```

---

## 課題2: less で長文を確認
### お題
1. 1〜30の行を含む `long.txt` を作成  
2. `less long.txt` で開く  
3. `/line25` と検索 → `n` で次の検索 → `q` で終了  

### コマンド
```bash
seq 1 30 | sed 's/^/line/' > long.txt
less long.txt
```

### 解説
- `less` 内操作  
  - スペース / ↓ : 下へ進む  
  - ↑ : 上に戻る  
  - `/文字列` : 検索  
  - `n` : 次の検索結果へ  
  - `q` : 終了  

---

## 課題3: wc で行数や文字数をカウント
### お題
1. `long.txt` の行数・単語数・バイト数を表示  
2. 行数だけ表示  
3. バイト数だけ表示  

### コマンドと実行結果
```bash
wc long.txt
wc -l long.txt
wc -c long.txt
```
```
30  30 201 long.txt
30 long.txt
201 long.txt
```

---

## 課題4: grep で検索
### お題
1. `app.log` を作成し、以下の内容を入れる  
   ```
   2025-08-31 OK started
   2025-08-31 ERROR db down
   2025-08-31 OK finished
   ```
2. `grep "ERROR" app.log` でエラー行のみ抽出  
3. `grep -in "error" app.log` で大文字小文字無視・行番号付き  
4. `grep -r "ERROR" logs` でディレクトリ検索  

### コマンドと実行結果
```bash
echo -e "2025-08-31 OK started\n2025-08-31 ERROR db down\n2025-08-31 OK finished" > app.log
grep "ERROR" app.log
grep -in "error" app.log
mkdir -p logs && cp app.log logs/
grep -r "ERROR" logs
```
```
2025-08-31 ERROR db down
2:2025-08-31 ERROR db down
logs/app.log:2025-08-31 ERROR db down
```

---

## 課題5: tail -f でログをリアルタイム追従
### お題
1. **ターミナルA** で `tail -f app.log` を実行  
2. **ターミナルB** で以下を追記  
   ```bash
   echo "2025-08-31 ERROR timeout" >> app.log
   echo "2025-08-31 OK retry" >> app.log
   ```
3. ターミナルAでリアルタイムに反映されることを確認  

### 実行結果（ターミナルA）
```
2025-08-31 OK started
2025-08-31 ERROR db down
2025-08-31 OK finished
2025-08-31 ERROR timeout
2025-08-31 OK retry
```

---


