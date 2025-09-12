# 12. ログ管理

Linux ではシステムやアプリの動作を記録するログが `/var/log` 以下に保存される。  
トラブルシューティングや監視で重要な役割を果たす。

---

## 課題1: ログファイルの場所を確認

### コマンド例
```bash
ls /var/log
```

### 主なログファイル
- `syslog` … システム全体の一般ログ  
- `auth.log` … 認証やログイン履歴、sudo 実行記録  
- `kern.log` … カーネル関連のメッセージ  
- `dpkg.log` … パッケージのインストール/削除履歴  
- `journal/` … systemd のジャーナルログ  
- `btmp` / `wtmp` / `lastlog` … ログイン成功/失敗履歴  

---

## 課題2: syslog の中身を確認

### コマンド例
```bash
tail -n 20 /var/log/syslog
```

### 出力例
```
wsl-pro-service[...] INFO Daemon: connecting to Windows Agent
systemd-resolved[...] Clock change detected. Flushing caches.
kernel: systemd-journald[...] Time jumped backwards, rotating.
```

- INFO / WARNING / DEBUG といったレベルで記録される  
- 最近のイベントを確認できる  
- `tail -f` を使えばリアルタイム監視も可能  

---

## 課題3: 認証ログを確認

### コマンド例
```bash
tail -n 20 /var/log/auth.log
```

### 出力例
```
login[313]: pam_unix(login:session): session opened for user kengumi1115(uid=1000)
systemd-logind[183]: New session 1 of user kengumi1115.
CRON[1179]: pam_unix(cron:session): session opened for user root(uid=0)
```

- ログインの成功/失敗、セッション開始/終了が記録される  
- sudo 実行や cron ジョブの動作もここに残る  
- 不正ログインの痕跡調査に役立つ  

---

## まとめ

- ログは `/var/log` に保存される  
- `syslog` → システム全体のイベント  
- `auth.log` → 認証・権限周り  
- `tail` / `tail -f` で末尾やリアルタイム監視が可能  
- ログを読むことでトラブルの原因やセキュリティ状況を把握できる  

