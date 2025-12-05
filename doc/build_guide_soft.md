# MoooseMiniのソフト面について

## 書き込みファイルの置き場
以下にファイルを置きます。  
https://github.com/ataruno/MoooseFree/tree/main/firmware

25/12/05時点の最新はGithub Actions#27
https://github.com/ataruno/MoooseFree/tree/main/firmware/MoooseFree_firmware_%2327

各ファイルの解説です。  
* 右手に書き込むのは"MoooseFree_right-seeeduino_xiao_ble-zmk.uf2"
* 左手に書き込むのは"MoooseFree_left-seeeduino_xiao_ble-zmk.uf2"
* マイコンをいったん初期状態に戻すときは"settings_reset-seeeduino_xiao_ble-zmk.uf2"
* 上記3つのファイルが入っているのが.zipファイル(MoooseFree_firmware_#27.zip)
![](build_guide_soft/2025-12-05-19-42-53.png)

## セキュリティの話
気にされている人がどこまでいるかわかりませんが、ちょっとセキュリティの話。  
気にならない人は読み飛ばしてOKです。

### Github Actionsで生成されたファイルか否かの確認(トレーサビリティ)
ZMK frimewareではGithub Actionsで書き込みファイルを生成できる仕組みが構築されています。  
ソースコードを編集しGithubのリポジトリを更新するとGithub Actionsが走り、最後にはzipがダウンロードできる状態になります。  
さて、頒布用にアップロードしたzipファイルが本当にGithub Actionsで生成されたファイルかどうか確認したいですね。  
もしかすると(そんなことはないはずだが)、悪意をもった誰かが書き込みファイルを改ざんしているかもしれない…。

## ハッシュ値の話
Github Actionsでファイルが生成されるとzipがダウンロードできる状態になります。  
このとき、このzipファイルに対してハッシュ値計算した値がGithub Actions画面上には表示されます。  
"firmware27のスクショ.png"の右下にある文字列です。  
sha256:59e0812805a39faae4c6a50fdb77c42abe087ae8977394aa329e928cfdb706a3
![](../firmware/MoooseFree_firmware_27/frimware27のスクショ.png)

ハッシュ値は元データに対して一意になるような計算がされます。  
また、ハッシュ値計算のアルゴリズムはオープンなものですので、自分で計算することも可能です。  
つまり、ユーザー自身がZipファイルのハッシュ値計算をして、Github Actionsで表示されているハッシュ値計算と合致すれば、両者はまったく同じファイルと言えるわけです。

Windowsは標準機能でハッシュ値計算ができるそうな。  
コマンドは以下。  
certutil -hashfile ＜ファイルパス＞ [ハッシュアルゴリズム]  
ということでやってみました。  
![](build_guide_soft/2025-12-05-19-48-32.png)

確かに同じ値になっていますね！  
これで安心して「あっ、このファイルはGithub Actionsで生成されたままの状態だな」とわかるわけです。  


