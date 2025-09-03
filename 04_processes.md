# 04. プロセス管理

Linuxでのプロセス操作の基本（ps / kill / top / jobs / fg / bg）の練習。

---

## 課題1: プロセスの一覧と終了
### お題
1. `sleep 60 &` を実行してバックグラウンドで開始  
2. `ps aux | grep sleep` で PID を確認  
3. `kill PID` で終了  
4. `ps aux | grep sleep` で消えたことを確認  

### コマンドと結果
```bash
sleep 60 &
ps aux | grep sleep
kill 668    # 例: PID が 668 の場合
ps aux | grep sleep
```
```
kengumi+     668  0.0  0.0   3124  1664 pts/0    S    21:42   0:00 sleep 60
kengumi+     671  0.0  0.0   4088  1920 pts/0    S+   21:43   0:00 grep --color=auto sleep
[1]+  Done                    sleep 60
```

---

## 課題2: top でリアルタイム監視
### お題
1. `top` を実行してプロセス一覧を確認  
2. CPU使用率やメモリ使用率を観察  
3. `q` で終了  

### コマンド
```bash
top
```

---

## 課題3: ジョブの管理
### お題
1. `sleep 100 &` でバックグラウンド開始  
2. `jobs` で確認  
3. `fg` でフォアグラウンドに戻す  
4. `Ctrl+Z` で一時停止  
5. `bg` でバックグラウンド再開  

### コマンドと結果
```bash
sleep 100 &
jobs
fg
^Z
bg
jobs
```
```
[1]+  Running                 sleep 100 &
[1]+  Stopped                 sleep 100
[1]+  Running                 sleep 100 &
[1]+  Done                    sleep 100
```

---

## 課題4: ジョブ番号で kill
### お題
1. `sleep 300 &` を実行  
2. `jobs` でジョブ番号を確認  
3. `kill %1` で終了  

### コマンドと結果
```bash
sleep 300 &
jobs
kill %1
jobs
```
```
[1]   Running                 sleep 300 &
[1]+  Terminated              sleep 300
```

---

