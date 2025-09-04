# 05. パッケージ管理

Linux でソフトウェアをインストール・アップデート・削除する基本を学ぶ。  
APT (Advanced Package Tool) を使った一連の流れを実演。

---

## 課題1: パッケージ情報の更新と候補の確認

### お題
1. `sudo apt update` でパッケージ情報を更新  
2. `apt list --upgradable` でアップデート候補を確認  
3. `apt search/show/policy` でインストール前にパッケージを調査  

### コマンド例
```bash
sudo apt update
apt list --upgradable
apt search tree
apt show tree
apt policy tree
```

---

## 課題2: パッケージを入れて使ってみる（例: tree）

### お題
1. `sudo apt install -y tree` でインストール  
2. `tree --version` / `which tree` で確認  
3. `tree -L 2 .` や `tree -a --dirsfirst` で実際に使ってみる  
4. `dpkg -L tree` で展開されたファイルを確認  

### コマンド例
```bash
sudo apt install -y tree
tree --version
which tree
tree ~ | head -n 40
tree -L 2 .
tree -a -L 1 --dirsfirst .
dpkg -L tree | head -n 20
```

> よく使うオプション:
> - `-L <n>`: 深さ n 階層まで表示  
> - `-a`: 隠しファイルも表示  
> - `--dirsfirst`: ディレクトリを先に表示  
> - `-I pattern`: 除外パターンを指定  

---

## 課題3: システム更新（upgrade と full-upgrade）

### お題
1. `apt list --upgradable` で候補を確認  
2. `sudo apt -s upgrade` でシミュレーション  
3. `sudo apt upgrade` で通常アップグレード  
4. `sudo apt -s full-upgrade` → `sudo apt full-upgrade` で依存も含めた更新  
5. `sudo apt autoremove --purge` で不要パッケージを削除  

### コマンド例
```bash
apt list --upgradable
sudo apt -s upgrade
sudo apt upgrade
sudo apt -s full-upgrade
sudo apt full-upgrade
sudo apt autoremove --purge
```

### Phased Updates（段階的配信）
実行時に以下のような表示が出る場合がある：

```
The following upgrades have been deferred due to phasing:
  libegl-mesa0 libgbm1 ...
```

- 一部のパッケージは安全性確認のため段階的に配信される  
- 原則は **待てばそのうち反映される**  
- どうしても必要なら自己責任で無視可能：  
  ```bash
  sudo apt -o APT::Get::Always-Include-Phased-Updates=true full-upgrade
  ```

---

## 課題4: アンインストール（remove と purge の違い）

### お題
1. `nano` を例に削除挙動を確認  
2. `remove` → 実体削除、設定ファイル残存（状態: rc）  
3. `purge` → 設定ファイルも完全削除（状態: un/pn）  

### コマンド例
```bash
# インストール
sudo apt install -y nano

# 設定ファイルを確認
dpkg -L nano | grep /etc

# remove: 実体のみ削除
sudo apt remove -y nano
dpkg -l nano

# purge: 設定も含めて完全削除
sudo apt purge -y nano
dpkg -l nano

# 復元したい場合
sudo apt install -y nano
```

### 状態フラグの見方
- `ii` : インストール済み  
- `rc` : remove 済み（実体なし・設定残り）  
- `un/pn` : 完全削除（設定も削除済み）  

---

## まとめ
- **update → list → install → upgrade → autoremove** が基本の流れ  
- `-s` シミュレーションで「何が起こるか」を必ず確認  
- `remove` と `purge` の違いは「設定ファイルを残すかどうか」  
- Phased Updates は慌てず待つのが基本  


