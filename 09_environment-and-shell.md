# 09. 環境変数とシェルの基礎

Linux でコマンドやプログラムの動作を制御する「環境変数」について学ぶ。  
代表例は **PATH**（コマンド検索パス）、**HOME**（ホームディレクトリ）、**LANG**（言語設定）。

---

## 課題1: 環境変数の確認

### コマンド例
```bash
echo $HOME     # ホームディレクトリ
echo $SHELL    # 現在使用しているシェル
echo $PATH     # コマンド検索パス
```

### 出力例
```
/home/kengumi1115
/bin/bash
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:...:/home/kengumi1115/myscripts
```

- `$HOME` … ユーザーのホームディレクトリ  
- `$SHELL` … 現在利用しているシェル（bash, zsh など）  
- `$PATH` … コマンドを探すディレクトリ一覧（: で区切る）  

---

## 課題2: 環境変数の設定

### コマンド例
```bash
export MYNAME="kengumi"
echo $MYNAME
```

出力例:
```
kengumi
```

- `export` を付けることで環境変数として登録され、子プロセスにも引き継がれる  

PATH にディレクトリを追加：
```bash
export PATH=$PATH:/home/kengumi1115/myscripts
```

---

## 課題3: 環境変数を利用したスクリプト

### スクリプト内容 (hello_env.sh)
```bash
#!/bin/bash
echo "Hello $USER, your home is $HOME"
echo "Your current PATH is: $PATH"
```

### 実行方法
```bash
chmod +x hello_env.sh
./hello_env.sh
```

### 出力例
```
Hello kengumi1115, your home is /home/kengumi1115
Your current PATH is: /usr/local/sbin:...:/home/kengumi1115/myscripts
```

- `$USER`, `$HOME`, `$PATH` といった環境変数をスクリプト内で活用可能  

---

## 課題4: 一時的な環境変数と export の違い

### 一時的に変数を渡す
```bash
MYTEMP="HelloEnv" env | grep MYTEMP
```
出力:
```
MYTEMP=HelloEnv
```
→ そのコマンドにだけ有効。`echo $MYTEMP` では何も出ない。

### export でセッション全体に有効化
```bash
export MYTEMP="PersistEnv"
echo $MYTEMP
env | grep MYTEMP
```
出力:
```
PersistEnv
MYTEMP=PersistEnv
```

---

## まとめ

- 環境変数はプログラムの動作を制御する重要な仕組み  
- `VAR=value command` … 一時的にそのコマンドにだけ有効  
- `export VAR=value` … シェル全体で有効、子プロセスにも引き継がれる  
- PATH に追加したディレクトリにスクリプトを置けば、どこからでも実行可能  


