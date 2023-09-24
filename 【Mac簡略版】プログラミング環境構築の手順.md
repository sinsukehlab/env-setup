# Mac 簡略版

やっていることの意味は分からなくていいから、具体的にすべきことだけ知りたい場合はこの手順を参照する。  
意味が知りたいときや、やり方が分からないとき、エラーが起こった際はリンク先の元のマニュアルを見ると詳しい説明が書かれている。

## 1. VSCode をインストールする

元マニュアル: [1.VSCode をインストールする](./1.VSCodeをインストールする.md)

1. [参考サイト](https://www.javadrive.jp/vscode/install/index1.html)の「Visual Studio Code をダウンロードする」と「Visual Studio Code をインストールする」の項を参考にインストールする。
2. インストールした VSCode を開き、  
   [shift + command + P] -> [shell command]と入力 -> [シェルコマンド：PATH 内に'code'コマンドをインストールします]を選択。

## 2. Git をインストールする

元マニュアル: [3.(Mac のみ)Git をインストールする](<./3.(Macのみ)Gitをインストールする.md>)

[参考サイト](https://prog-8.com/docs/git-env)を参考にインストールする。  
なお、現時点ではユーザー名とメールアドレスの設定まではしなくても、ターミナル上で`git --version`を入力して Enter を押したときにバージョンが表示されれ(エラーが起こらなけれ)ばよい。

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
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install coreutil
```

## 4. Anaconda をインストールする

元マニュアル: [5.Anaconda をインストールする](./5.Anacondaをインストールする.md)

[参考サイト](https://www.python.jp/install/anaconda/macos/install.html)の「パッケージのダウンロード」と「パッケージのインストール」を参考にインストールする。  
その後、ターミナルで下記を実行する。

```shell
/opt/anaconda3/bin/conda init zsh
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
    sh = stash
    su = stash -u
    svu = stash save -u
    sp = stash pop
```
