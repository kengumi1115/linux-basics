# 11. ネットワーク関連コマンド

Linux ではネットワーク状態や疎通確認を行うために様々なコマンドが利用できる。

---

## 課題1: ネットワーク設定の確認

### コマンド例
```bash
ip addr
```

### 出力例
```
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> ...
    inet 172.20.66.237/20 brd 172.20.79.255 scope global eth0
```

- `lo` … ループバック (127.0.0.1)  
- `eth0` … 実際のネットワークカード  
- `inet` … IPv4 アドレス  
- `inet6` … IPv6 アドレス  

---

## 課題2: 接続確認 (ping)

### コマンド例
```bash
ping -c 4 8.8.8.8
```

### 出力例
```
4 packets transmitted, 4 received, 0% packet loss
rtt min/avg/max/mdev = 6.358/6.696/6.990/0.292 ms
```

- `-c 4` … 4回だけ送信  
- 0% packet loss → 通信が安定している  

---

## 課題3: 名前解決の確認

### コマンド例
```bash
ping -c 4 google.com
```

### 出力例
```
PING google.com (172.217.175.110) ...
```

- DNS によって **google.com → IPアドレス** に変換された  
- 名前解決が正常に動いていることを確認できる  

---

## 課題4: ネットワーク接続の状態確認

### コマンド例
```bash
ss -tuln
```

### 出力例
```
udp UNCONN 0 0 127.0.0.53:53   0.0.0.0:*
tcp LISTEN 0 1000 10.255.255.254:53 0.0.0.0:*
```

- `t` = TCP, `u` = UDP, `l` = listen, `n` = 数字で表示  
- ポート53 → DNS  
- ポート323 → NTP  

---

## まとめ

- `ip addr` … IPアドレスやNICの情報を確認  
- `ping` … ネットワーク疎通確認（IPアドレスやドメインで試せる）  
- `ss -tuln` … 現在待ち受けているポートや接続を確認  
- DNSの名前解決と疎通確認を組み合わせて、問題の切り分けが可能  

