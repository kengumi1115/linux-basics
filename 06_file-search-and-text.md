# 06. ファイル検索とテキスト処理

Linux でファイルやテキストを検索する方法を学ぶ章。  
主に **grep** と **find** を利用し、組み合わせて強力な検索を行う。

---

## 課題1: grep の基本

### コマンド例
```bash
# サンプルファイル作成
echo -e "apple\nbanana\norange\napple pie\npineapple" > fruits.txt
cat fruits.txt

# apple を含む行を検索
grep apple fruits.txt

# 大文字小文字を無視して検索
grep -i APPLE fruits.txt

# 行番号を表示
grep -n apple fruits.txt

# apple を含まない行を表示
grep -v apple fruits.txt
```

---

## 課題2: find の基本

### コマンド例
```bash
# ホーム以下で fruits.txt を探す
find ~ -name "fruits.txt"

# 拡張子 txt のファイルを探す
find ~ -name "*.txt"

# ディレクトリだけ探す
find ~ -type d -name ".*"

# サイズで検索 (1MB以上)
find ~ -size +1M

# 見つかったファイルに対して ls -l を実行
find ~ -name "*.txt" -exec ls -l {} \;
```

---

## 課題3: find と grep の組み合わせ

### コマンド例
```bash
# ホーム以下の txt から apple を探す
find ~ -name "*.txt" -exec grep -n --color=auto apple {} \;

# カレント以下から apple を探す (ファイル名も表示)
find . -name "*.txt" -exec grep -Hn apple {} \;

# 大文字小文字無視で検索
find ~ -name "*.txt" -exec grep -iHn apple {} \;
```

---

## 課題4: 応用例

### コマンド例
```bash
# apple を含む行数をカウント
grep -i apple fruits.txt | wc -l

# apple または banana を検索 (拡張正規表現)
grep -E "apple|banana" fruits.txt

# 除外検索 (ログや.gitを除外)
grep -rn --color=auto "apple" . --exclude="*.log" --exclude-dir=".git"

# find + grep + wc で総行数をカウント
find ~ -name "*.txt" -exec grep -i "apple" {} \; | wc -l
```

---

# grep チートシート

## 基本オプション
| オプション | 意味 | 例 |
|------------|------|----|
| `-i` | 大文字小文字を無視 | `grep -i apple fruits.txt` |
| `-n` | 行番号を表示 | `grep -n apple fruits.txt` |
| `-H` | ファイル名を常に表示 | `grep -H apple fruits.txt` |
| `--color=auto` | マッチ部分を色付き表示 | `grep --color=auto apple fruits.txt` |

## ファイル/ディレクトリ関連
| オプション | 意味 | 例 |
|------------|------|----|
| `-r` | ディレクトリを再帰的に検索 | `grep -r apple .` |
| `-R` | シンボリックリンクも含めて再帰 | `grep -R apple /etc` |
| `--exclude="*.log"` | 特定ファイルを除外 | `grep -rn apple . --exclude="*.log"` |
| `--exclude-dir=".git"` | 特定ディレクトリを除外 | `grep -rn apple . --exclude-dir=".git"` |

## パターン検索
| オプション | 意味 | 例 |
|------------|------|----|
| `-E` | 拡張正規表現 (egrep 相当) | `grep -E "apple|banana" fruits.txt` |
| `-v` | マッチしない行を表示 | `grep -v apple fruits.txt` |
| `-w` | 単語単位で検索 | `grep -w apple fruits.txt` |
| `-c` | マッチ行数を表示 | `grep -c apple fruits.txt` |
| `-l` | マッチしたファイル名のみ表示 | `grep -l apple *.txt` |
| `-L` | マッチしなかったファイル名のみ表示 | `grep -L apple *.txt` |

---

# grep オプション略語の意味

| オプション | 英語の略 | 意味 |
|------------|----------|------|
| `-i` | *ignore case* | 大文字小文字を無視する |
| `-n` | *number* | 行番号を表示する |
| `-H` | *filename* | ファイル名を常に表示する |
| `-r` | *recursive* | ディレクトリを再帰的に検索する |
| `-R` | *recursive (follow symlinks)* | 再帰検索＋シンボリックリンクもたどる |
| `-E` | *Extended regex* | 拡張正規表現を使う |
| `-v` | *invert match* | マッチを反転 |
| `-w` | *word-regexp* | 単語単位で検索 |
| `-c` | *count* | マッチ行数を数える |
| `-l` | *list files* | マッチしたファイル名のみ表示 |
| `-L` | *list non-matching files* | マッチしなかったファイル名のみ表示 |

---

## まとめ
- **grep** はファイル内容検索、**find** はファイル自体の検索  
- 両者を組み合わせることで「大量ファイルから特定の行を探す」ことが可能  
- オプションはチートシートを活用して暗記負担を減らす  


