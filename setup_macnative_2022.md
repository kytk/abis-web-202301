# macOS native 環境での ABiS チュートリアルの準備方法
 
## 目次

- [はじめに](#anchor0)
- [前提条件](#anchor1)
- [インストールが必要なソフトウェア](#anchor2)
- [ソフトウェア毎のインストールおよび確認方法](#anchor3)
- [問い合わせ](#anchor5)


<a id="anchor0"></a>
## はじめに

- **チュートリアルの準備には、約1-2時間必要となります。時間に十分に余裕をもって>準備をされてください。特に、macOS native環境では、想定通りにうまくいかないことも十分考えられます。このため、早めの準備をお願いします。なお、準備が終わった方にのみ当日のSlackのリンクが表示されますので、必ず準備を行ってください。準備なしの参加はできません**

- 本セクションでは、Lin4Neuro を使わずに、macOS native 環境でのチュートリアルのセットアップ方法を記載します。Apple M1/M2 でも対応可能です。ただし、この方法でのセットアップのサポートは限られることをご了承ください(個人個人で環境がかなり異なるためです)。このインストラクションを読んでわからないことが多い方は、ご自身でのセットアップは難しいとお考えいただき、Lin4Neuroでの受講としてください

- チュートリアルに十分な環境で参加していただくために、下記を参照のうえ、受講環境を整えてください。その後、https://kytk.github.io/abis-web-202212/ に戻っていただき、「チュートリアルテキストの入手」に進んでください

- データを入手し、受講のためのスクリプトを実行し、その値が正しい場合に限り、当日のSlackのアドレスをお伝えします。**2022年12月4日までに**必ずテスト解析まで終わらせてください。テストスクリプトを実行できた方が受講できます。セットアップがうまくいかない方はサポートしますので、早めにご連絡ください。サポート窓口は、このページの一番下にあります。

<a id="anchor1"></a>
## 前提条件

- CPUは Intel でも Apple M1/M2 でも問いません
- ターミナルはデフォルトの zsh でなく bash を使用することとします。ターミナルから以下のようにタイプしてください。

    ```
    echo $SHELL
    ```

- この結果が、/bin/bash (もしくは/usr/local/bin/bash) でない方は、以下のコマンドをタイプしてください

    ```
    chsh -s /bin/bash
    ```

- この後、ターミナルを起動し直すと、bashに変わります。確認のためには、`echo $SHELL` を実行し、その結果が /bin/bash であることを確認してください

- この場合、システムレベルの /etc/zshrc (キーバインディング等) や、~/.zshrc.profile にて個人的に設定している内容は反映されなくなるので注意してください

- zsh に戻したい場合は、いつでも `chsh -s /bin/zsh` で zsh に戻すことができます

<a id="anchor2"></a>
## インストールが必要なソフトウェア
- git
- Matlab
- SPM
- CONN

<a id="anchor3"></a>
## ソフトウェア毎のインストールおよび確認方法


### 1. git (バージョン指定なし)

#### 1.1. インストール
- Command line tools for Xcode のインストールにより git を使うことが可能となります

    ```
    xcode-select --install
    ```

#### 1.2. 確認
- ターミナルから以下をタイプしていただき、バージョンが出力されれば大丈夫です

    ```
    git --version
    ```


### 2. SPM12 と CONN21.a : Matlab をお持ちの場合
- SPM と CONN はMatlabを持っているか持っていないかでインストールの方法が変わります。Matlab をお持ちでない方は、次の 16. SPM と CONN: Matlab をお持ちでない場合 に従ってセットアップをしてください

- Apple M1/M2 は、Matlab R2020b 以降でないと動作しませんのでご注意ください

#### 2.1. SPM12のインストール
- GitHub経由が便利です
- ホームディレクトリの下に spm12 をインストールすることとします

    ```
    cd #ホームディレクトリに移動します
    git clone https://github.com/spm/spm12.git
    ```

- SPMはmacOSのセキュリティで実行できないことがあるため、この問題を回避するために、ターミナルから以下を実行します

    ```
    sudo xattr -r -d com.apple.quarantine ~/spm12
    sudo find ~/spm12 -name '*.mexmaci64' -exec spctl --add {} \;
    ```

- この後、Matlabのパス設定で、/Users/ご自分のユーザ名/spm12 を指定してください

#### 2.2. SPM12の確認
- Matlab から

    ```
    spm
    ```

とタイプし、SPMが起動すればOKです

#### 2.3. CONN 21.a のインストール
- 異なるバージョンを使うことができるように、ホームディレクトリの下に conn を作成し、その下に、conn21a をインストールすることにします

- ターミナルで以下をタイプします

    ```
    cd ~/Downloads
    curl -O https://www.nitrc.org/frs/download.php/12426/conn21a.zip
    mkdir conn21a
    unzip conn21a.zip -d conn21a
    cd conn21a
    mv conn conn21a
    [ ! -d ~/conn ] && mkdir ~/conn
    cp -r conn21a ~/conn
    ```

- その後、Matlab のパス設定で、/Users/ご自分のユーザ名/conn/conn21a を指定してください

#### 2.4. CONN 21.a の確認
- Matlabから

    ```
    conn
    ```

とタイプし、CONNが起動すればOKです


### 3. SPM12 と CONN21.a : Matlab をお持ちでない場合

- チュートリアル用に SPM12 と CONN21.a を Matlab がなくても動作するようにスタンドアロン版を作成しました。以下に従ってセットアップを行ってください

#### 3.1. Matlab Runtime R2020b の入手

- ターミナルに以下を入力し、Matlab Runtime R2020b を入手します。Intel Mac, Apple M1 ともに共通です。

    ```
    cd ~/Downloads
    curl -O https://ssd.mathworks.com/supportfiles/downloads/R2020b/Release/8/deployment_files/installer/complete/maci64/MATLAB_Runtime_R2020b_Update_8_maci64.dmg.zip
    unzip MATLAB_Runtime_R2020b_Update_8_maci64.dmg.zip
    ```

- ダウンロードフォルダにある MATLAB_Runtime_R2020b_Update_8_maci64.dmg をダブルクリックします

- InstallForMacOSX をダブルクリックします。**インストール先はデフォルトのまま変更しないでください**

#### 3.2. SPM12 standalone のインストール

- 以下で SPM12 standalone を入手し、/opt の下にインストールします。

    ```
    cd ~/Downloads
    curl -O https://www.nemotos.net/l4n-abis/macOS/spm12_standalone_maci64_v99.zip
    sudo unzip spm12_standalone_maci64_v99.zip -d /opt/
    echo "" >> ~/.bash_profile
    echo "# Alias for SPM12" >> ~/.bash_profile
    echo "alias spm='/opt/spm12_standalone/run_spm12.sh /Applications/MATLAB/MATLAB_Runtime/v99'" >> ~/.bash_profile
    ```

- 一度ターミナルを閉じます。

#### 3.3. SPM12 standalone の確認

- ターミナルを起動した後、spm と入力すればSPMが起動します。ただ、初回は起動するまでに数分時間がかかるため、焦らずにお待ちください


    ```
    spm
    ```

#### 3.4. CONN 21.a standalone のインストール

- CONN は以下の方法でインストールできます

    ```
    cd ~/Downloads
    curl -O https://www.nemotos.net/l4n-abis/macOS/conn21a_standalone_maci64_v99.zip
    unzip conn21a_standalone_maci64_v99.zip -d /Applications/
    echo "" >> ~/.bash_profile
    echo "# Alias for CONN 21.a" >> ~/.bash_profile
    echo "alias conn='/Applications/conn21a_standalone/run_conn.sh /Applications/MATLAB/MATLAB_Runtime/v99'" >> ~/.bash_profile
    ```

- ターミナルを一度終了します

#### 3.5. CONN 21.a standalone の確認

- GUIとコマンドラインのどちらからも起動できます

- GUI の場合は、アプリケーションの中にある conn21a_standalone の中の conn をダブルクリックしてください

- ターミナルの場合は、ターミナルから conn とタイプすれば起動します

    ```
    conn
    ```



<a id="anchor5"></a>

## 問い合わせ

- 準備がうまくいかない時のために、問い合わせフォームを準備しています。こちらから
ご質問ください。数日以内に担当者から返信させていただきます

- [問い合わせフォーム](https://forms.gle/CniDGw5J1BSxEqjn9){:target="_blank"} 

