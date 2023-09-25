# Windows 簡略版

やっていることの意味は分からなくていいから、具体的にすべきことだけ知りたい場合はこの手順を参照する。  
意味が知りたいときや、やり方が分からないとき、エラーが起こった際はリンク先の元のマニュアルを見ると詳しい説明が書かれている。

## 1. VSCode をインストールする

元マニュアル: [1.VSCode をインストールする](./1.VSCodeをインストールする.md)

[参考サイト](https://www.javadrive.jp/vscode/install/index1.html)の「Visual Studio Code をダウンロードする」と「Visual Studio Code をインストールする」の項を参考にインストールする。

## 2. WSL2 をインストールする

元マニュアル: [2.(Windows のみ)WSL2 をインストールする](<./2.(Windowsのみ)WSL2をインストールする.md>)

1. ターミナルを開く  
   [スタート] -> [すべてのアプリ] –> [ターミナル]をクリック

2. 下記をターミナルにコピペして Enter を押し、処理が終わったら、パソコンを再起動する。  
   その後開いたターミナルで Linux のアカウントを作る。

```shell
wsl --install -d Ubuntu-22.04
```

3. ターミナルが下の正しい方のように表示されているのを確認する。

```shell
# 正しい方
アカウント名@パソコン名:~$

# 間違っている方
PS C:\Users\Windowsのユーザー名>

# 間違っていた場合下記を実行
wsl
```

4. その後、下記をターミナルにコピペして Enter。  
   最後に設定画面が表示されたら、`2`と入力する。

```shell
sudo apt -y update
sudo apt -y upgrade
sudo apt -y install zsh
chsh -s $(which zsh)
zsh
```

## 3. Oh My Zsh をインストールする

元マニュアル: [4.Oh My Zsh をインストールする](<./4.Oh My Zshをインストールする.md>)

1. 下記をコピペして Enter。  
   デフォルトシェルを Zsh にするか聞かれた場合は`y`と入力して Enter.  
   うまくいかないときは URL が変わっているかもしれないので、[公式サイト](https://ohmyz.sh/#install)を見る。

```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

2. 以下を実行。

```shell
cd ~/.oh-my-zsh/plugins/
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
git clone https://github.com/zsh-users/zsh-completions.git
git clone https://github.com/zsh-users/zsh-autosuggestions.git
git clone https://github.com/zsh-users/zsh-history-substring-search.git
cd ~
git clone --recursive https://github.com/philip82148/simplerich-zsh-theme
cp ./simplerich-zsh-theme/simplerich.zsh-theme ~/.oh-my-zsh/themes/
```

3. 下記を実行して VSCode で`~/.zshrc`というファイルを開く。

```shell
code ~/.zshrc
```

4. `ZSH_THEME="robbyrussell"`という行を探し、以下の 2 行に置き換え、Ctrl+S/Command+S で保存。  
   その後、VSCode を閉じる。

```shell
ZSH_THEME="simplerich"
source ~/simplerich-zsh-theme/zsh-git-prompt/zshrc.sh
```

5. 下記をターミナルで実行する。

```shell
source ~/.zshrc
sudo apt -y install bc
```

## 4. Anaconda をインストールする

元マニュアル: [5.Anaconda をインストールする](./5.Anacondaをインストールする.md)

以下を実行する。  
URL は最新版ではない可能性があるので、エラーになるときは[参考サイト](https://www.salesanalytics.co.jp/datascience/datascience141/#LinuxAnaconda)を見て最新版を取得する。  
途中`Please, press ENTER to continue`と言われたら Enter を押し、下矢印キーでライセンス条項を一番下まで降り、yes と入力して Enter を押す。  
次にインストール場所を聞かれるが、デフォルトのままでよいのでそのまま Enter を押す。  
最後に、Anaconda3 の初期化をするか聞かれるので、yes と答える。

```shell
cd ~
wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh
bash Anaconda3-2022.10-Linux-x86_64.sh
conda config --set changeps1 False
source ~/.zshrc
```

## 5. Git エイリアスを設定する

元マニュアル: [6.Git エイリアスを設定する](./6.Gitエイリアスを設定する.md)

1. ターミナルを開き、下記を実行して、VSCode で`~/.gitconfig`というファイルを開く。

```shell
code ~/.gitconfig
```

2. 下記を一番下に追記して、 Ctrl+S/Command+S で保存。

```shell
[alias]
    a = add
    c = commit
    cm = commit -m
    ad = commit --amend
    adm = commit --amend -m
    b = branch
    co = checkout
    cob = checkout -b
    sl = stash list
    su = stash -u
    svu = stash save -u
    sp = stash pop
```

## 6. VSCode の設定をする

元マニュアル: [7.VSCode の設定をする](./7.VSCodeの設定をする.md)

1. 以下をターミナル(WSL)上で実行し VSCode を**WSL 上で**開く。

```shell
code ~
```

2. [公式サイト](https://learn.microsoft.com/ja-jp/power-pages/configure/vs-code-extension#install-visual-studio-code-extension)の「Visual Studio Code 拡張機能のインストール」の項を参考に、以下の拡張機能を検索窓で検索して全てインストールする。

- Prettier - Code formatter (コードフォーマッタ)
- Black Formatter (Python のコードフォーマッタ)
- Code Spell Checker (英語のタイポを教えてくれる)
- Git Lens (Git 情報を見やすくしてくれる)
- Git History (Git のログを見やすくしてくれる)
- Code Runner (コードの(コンパイルと)実行をショートカットキーで行えるようにする)

3. VSCode 上で[Ctrl+,]/[Command+,] -> "Format On Save"と検索してチェックを入れる。
4. 続けて"Default Formatter"と検索して Prettier を選ぶ。
5. [ctrl+shift+P]/[command+shift+P]->[Reload Window]を選択。
