# 13. ストレージ管理

Linux ではディスク使用量の確認や、デバイスのマウント状況を調べることができる。

---

## 課題1: ディスク全体の使用量を確認

### コマンド
```bash
df -h
```

### 出力例
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/sdd       1007G  1.9G  954G   1% /
C:\             238G  188G   50G  80% /mnt/c
D:\             932G  388G  544G  42% /mnt/d
```

- **df** = *disk free*  
- `-h` = human-readable（MB/GB単位で表示）  
- マウントポイントごとの使用量・空き容量がわかる  

---

## 課題2: ディレクトリごとの容量を確認

### コマンド
```bash
du -sh /var/log
```

### 出力例
```
401M    /var/log
```

- **du** = *disk usage*  
- `-s` = summary（合計のみ）  
- `-h` = human-readable  
- `sudo` を付けると権限のあるディレクトリも確認可能  

---

## 課題3: マウントされているデバイスを確認

### コマンド
```bash
mount | grep "^/dev"
```

### 出力例
```
/dev/sdd on / type ext4 (rw,relatime,...)
/dev/sdd on /mnt/wslg/distro type ext4 (ro,relatime,...)
```

- **/dev/sdd** … デバイス名（WSL の仮想ディスク）  
- **on /** … マウントポイント  
- **type ext4** … ファイルシステム形式  
- **rw/ro** … 読み書き可能かどうか（rw=read/write, ro=read-only）  

---

## まとめ

- `df -h` … ディスク全体の使用量を確認 (*disk free*)  
- `du -sh ディレクトリ` … ディレクトリ単位の使用量を確認 (*disk usage*)  
- `mount` … どのデバイスがどこにマウントされているか確認  
- 権限が必要な場合は `sudo` を活用  


