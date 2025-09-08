# 08. ユーザーとグループ管理の応用

Linux におけるユーザーとグループ管理の応用操作を学ぶ章。  
03章で扱った基礎を発展させ、実務シナリオを想定して権限をコントロールする。

---

## 課題1: 自分のユーザー情報を確認

### コマンド例
```bash
whoami
id
groups
```

### 出力例
```
kengumi1115
uid=1000(kengumi1115) gid=1000(kengumi1115) groups=1000(kengumi1115),27(sudo),...
kengumi1115 adm cdrom sudo dip plugdev users
```

- **whoami** : 現在ログインしているユーザー名を表示  
- **id** : UID, GID, 所属グループを確認  
- **groups** : 所属グループ名の一覧  

---

## 課題2: アクセス制御シナリオ

### シナリオ
- **shared.log** : グループで共有（users グループ書き込み可）  
- **config.cfg** : 本人だけ編集可能  

### コマンド例
```bash
# サンプル作成
echo "ログ内容" > shared.log
echo "設定内容" > config.cfg

# グループ共有用 (rw-rw-r--)
chmod 664 shared.log
chgrp users shared.log

# 本人専用 (rw-------)
chmod 600 config.cfg

# 確認
ls -l shared.log config.cfg
```

出力例:
```
-rw-rw-r-- 1 kengumi1115 users       13 Sep  8 22:23 shared.log
-rw------- 1 kengumi1115 kengumi1115 13 Sep  8 22:23 config.cfg
```

---

## 課題3: sudo の利用

### コマンド例
```bash
ls /root          # 一般ユーザーでは Permission denied
sudo ls /root     # sudo を付けると実行可能
```

- `sudo` = superuser do  
- `/etc/sudoers` に登録されたユーザーだけ利用可能  

---

## 課題4: チーム用ディレクトリの設定

### シナリオ
- `project/` ディレクトリを作成  
- グループ (users) のメンバーは編集可能  
- その他ユーザーは閲覧のみ  

### コマンド例
```bash
mkdir project
sudo chgrp users project
chmod 2775 project   # setgid + rwxrwxr-x

ls -ld project
```

出力例:
```
drwxrwsr-x 2 kengumi1115 users 4096 Sep  8 22:40 project
```

- **2 (setgid)** を付けると、配下のファイル・ディレクトリが自動で `users` グループを継承  

---

## 特殊ビットまとめ

| 値 | 名前 | 意味 | 例 |
|----|------|------|----|
| **1** | sticky | ディレクトリ内のファイルを所有者以外削除不可 | `/tmp` |
| **2** | setgid | 配下のファイル/dir がグループを継承 | `project/` |
| **4** | setuid | 実行時に所有者権限で実行 | `/usr/bin/passwd` |

権限表示での例：  
- sticky → `drwxrwxrwt`  
- setgid → `drwxrwsr-x`  
- setuid → `-rwsr-xr-x`  

---

## まとめ

- `whoami`, `id`, `groups` でユーザーとグループを確認  
- `chmod` 数値指定で柔軟な権限管理（644, 600, 775 など）  
- `sudo` で必要な時だけ root 権限を利用  
- setgid を使うことでチーム用ディレクトリの管理が容易に  
- sticky, setuid, setgid など特殊ビットの知識も重要  

