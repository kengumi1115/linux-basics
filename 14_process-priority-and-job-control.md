# 14. プロセスの優先度とジョブ制御

Linux ではプロセスの「優先度 (priority)」を調整することができ、CPU の割り当てを制御できる。
優先度は **nice 値 (NI)** として管理され、数値が小さいほど優先度が高い。

- nice 値の範囲: `-20` (最高優先度) ～ `19` (最低優先度)
- デフォルト値: `0`

---

## 課題1: nice で優先度を指定して実行

### コマンド
```bash
nice -n 10 sleep 100 &
ps -l
```

### 出力例
```
0 S  1000     768     379  0  90  10 -   781 hrtime pts/0    00:00:00 sleep
```
- `NI` が **10** → デフォルト(0)より低い優先度で実行されている。

---

## 課題2: renice で実行中プロセスの優先度を変更

### コマンド
```bash
sleep 200 &
ps -l
sudo renice -n -5 -p <PID>
ps -l
```

### 出力例
```
1294 (process ID) old priority 0, new priority -5
0 S  1000    1294     379  0  75  -5 -   781 hrtime pts/0    00:00:00 sleep
```
- `NI` が **-5** → 優先度が上がっている。  
- **注意**: 優先度を上げる (負の nice 値) には root 権限が必要。

---

## 課題3: fg/bg とジョブ制御

### コマンド
```bash
sleep 300
# Ctrl+Z で一時停止
bg
jobs
ps -l | grep sleep
sudo renice -n -10 -p <PID>
fg
```

### 出力例
```
[1]+  Stopped   sleep 300
[1]+  Running   sleep 300 &
1462 (process ID) old priority 0, new priority -10
```
- `jobs` → バックグラウンドジョブ一覧を表示  
- `bg` → 停止中ジョブをバックグラウンドで再開  
- `fg` → バックグラウンドジョブをフォアグラウンドに戻す  

---

## まとめ

- `nice -n 値 command` … 指定した優先度でコマンド実行  
- `renice -n 値 -p PID` … 実行中プロセスの優先度を変更  
- 優先度を上げる (負の値) には `sudo` が必要  
- `jobs` / `fg` / `bg` … ジョブ制御でフォアグラウンド・バックグラウンドを切り替え可能  


