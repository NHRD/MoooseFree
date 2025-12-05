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

### Github Actionsで生成されたファイルか否かのトレーサビリティ
Github Actionsでファイルが生成されるとzipがダウンロードできる状態になります。  
このとき、このzipファイルに対してハッシュ値計算した値がGithub Actions画面上には表示されます。
"firmware#27のスクショ.png"の右下にある羅列です。
sha256:59e0812805a39faae4c6a50fdb77c42abe087ae8977394aa329e928cfdb706a3
![](../firmware/MoooseFree_firmware_#27/frimware#27のスクショ.png)

ハッシュ値計算のアルゴリズムがSHA256を使われています。  
ハッシュ値は元データに対して一意になるような計算がされます。  
さて、このリポジトリにアップしたzipファイルが本当にGithub Actionsで生成されたファイルかどうか確認したいですね。  
Github Actionsで生成されたファイルを改ざんして変なものを埋め込まれていたりしない？？？
そんなことはないですが、セキュリティ観点としては"何も信用しない"が前提となります。(ゼロトラスト)

![](build_guide_soft/2025-12-05-19-48-32.png)

