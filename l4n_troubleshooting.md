# Lin4Neuroがインポートできない場合

0x80004005 などのエラーでLin4Neuroが起動できない、もしくはインポートできない場合は、以下を試してください

## 準備

- VirtualBox 7.0.2 以降はインストールされている前提でいきます

- エラーとなったLin4Neuroは右クリック -> 除去 -> すべてのファイルを削除 から削除してください

- ovaファイルを保存するフォルダを作成してください。ここでは、l4n-ova というフォルダを作成すると仮定します

    ```
    mkdir l4n-ova
    ```

- 以下のリンクから、L4N-2004-ABIS-20221107-disk001.vmdk をダウンロードし、このl4n-ovaフォルダの中に保存します

    https://www.dropbox.com/t/uYIYllcbIyhIMXxL


## VirtualBoxへの登録
- VirtualBoxマネージャーで、「新規」をクリックします

    ![新規](img/vb_t01.png)

- 以下を設定します
    - 名前: L4N-2004-ABIS-2212 としてください
    - Folder: 自分がインストールしたいフォルダ (250GB以上空き容量があるところ) を指定してください
    - タイプ: Linux を選んでください
    - バージョン: Ubuntu (64-bit) を選択してください
    - ここまで選んだら「次へ」をクリックします

    ![OS](img/vb_t02.png)

- メモリは 4096MB、CPUは2を設定して「次へ」をクリックしてください(任意ですが、まずはこれで)

    ![memory](img/vb_t03.png)

- Virtual Hard disk の画面では、"Use an Existing Virtual Hard Disk File" を選び、その右側のフォルダアイコンをクリックしてください

    ![vhd1](img/vb_t04.png)

- ハードディスク選択の画面で、「追加」をクリックし、先程展開した L4N-2004-ABIS-20221107-disk001.vmdk を選びます

    ![vhd2](img/vb_t05.png)

- そうすると、Not attached のところにL4N-2004-... があらわれるので、それを選択して"Choose" をクリックしてください

    ![vhd3](img/vb_t06.png)

- 今選択したハードディスクが表示されていることを確認してから、次へをクリックします

    ![vhd4](img/vb_t07.png)

- これで「完了」を押すと完了です

    ![finish](img/vb_t08.png)

- 選択して起動するかどうかを確認してください

    ![run](img/vb_t09.png)


