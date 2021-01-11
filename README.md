﻿# YS2EDIT_MSX2
 Ys2 Message Editor for MSX2

## これはなに？

イース２のディスクの中にあるメッセージデータを表示したり編集するツールです。
何の役に立つかというと、ネタ用です。

ディレクトリ表示から該当セクタへ飛ぶ機能はありますが、
実質的には（文字表示・入力タイプの）ただのセクタ単位バイナリエディタです。

MSX2以上/MSXDOS1/MSXDOS2モード対応
ターボRなら高速モードで動作可能です。
（基本がBASICで組まれていて遅いのでターボRがお勧めです）



## 注意事項

ディスクを書き換えるので、オリジナルディスクは使わずに
バックアップしたディスクを使ってください。

間違ってオリジナルディスクを壊してしまうなどの問題が発生しても
当方は一切責任を負えませんので、その点は気を付けてご利用ください。

（プロテクトの外し方などは自分でお調べください）
（オリジナルで起動してから入れ替えてもある程度はいけます）

ツールとしての出来もイマイチなので、
なんでもいいから弄ってみたいという人向けです。
実機で弄ることにロマンを感じる人向け。

同梱のフォント画像を参考にコード変換すれば
Windows等でもツールは作れるのではないかと思います。
Windows上で編集するツール作った方が快適に弄れると思います。


## 起動

DSKイメージをBlueMSXやOpenMSXやWebMSXにセットするか、
FDDに書き出して実機にセット。

RUN"YS2MEDIT"

エディターの画面がでたら、イース2のプログラムディスクやデータディスクに入れ替えてください。

|コマンド|内容 |
|--|--|
|1.READ  | 指定したセクタを読み込みます。24セクタ単位です。|
|2.WRITE | 読み込み済みのデータを書き戻します。|
|3.EDIT  | 読み込んだデータを表示・編集します。|
|4.DIR   | イースファイルシステムのファイルリストを読み込んで表示します。<br>ファイルを選択すると該当セクタを読み込んでEDIT画面へ移動します|

- ※ Y/Nの入力を求められたときは、かなを解除してください。

- 編集したデータがある場合、READ前に保存するか問い合わせます
- 読み込んだデータがないとEIDTできません
- 保存時は、編集してない場合、読み込んでない場合に警告が出ます（書き込み中止はしません）


## EDIT説明

- ESC：EDITを抜ける

- INS：1セクタ進む
- DEL：1セクタ戻る

- SELECT：フォントの種類を変える（ゲームフォント/タイトル&エンディングフォント/一般MSXフォント）

- HOME: そのセクタの先頭にカーソルが移動
- CLS（SHIFT+HOME）： 現在読み込んでいるセクタの先頭に移動

- RETURN：入力モード変更（通常/数値入力）

- カーソルキー：カーソルの移動

通常入力モード時：
- それ以外のキー：文字入力

数値入力モード時：
- 詳細は次の項目参照

注意：

     （かなONの時はアルファベットが入力されないので注意）


## 数値入力モード（CODE MODE）

16進数の上位4ビットは+/-キーで変更します。

（TABのあとに0～9、A～Fでも変更可能）
（現在の一覧が表示されています）

0～9、A～Fを押すと、該当する文字が入力されます。

RETURNを押すと通常入力モードに戻ります。


---
## ■ ツール紹介

- ys2_extract.exe  
同梱のツール。srcフォルダにソース有。  
イース2のディスクをドロップすると、中のファイルを取り出します。
実験用。

- DiskExplorer  
    https://hp.vector.co.jp/authors/VA013937/editdisk/index.html  
    dskイメージを開き、ファイルを出し入れするツール  

- MSXVIEWer  
    https://www.minagi.jp/2004/05/20/msxviewer/  
    BASやSC5ファイルを表示するツール  
    BASファイルをTXT形式に変換保存もできます。  

    *(※半角ひらがなやグラフィック文字は全角に変換されます。)*

    MSXBASIC上で ``SAVE"ファイル名",A`` としてもテキスト形式で保存できます。



---
## ■ DSKイメージ内のファイル解説

- MSX2ASM  
    ...MSX2 Simple ASM  
    （バックアップ活用テクニック PART16掲載。POCO氏制作「アセンブルシステム」）  

- YS2MEDIT  
    ...エディタの起動プログラム。RUN"YS2MEDIT"で実行。  

- YS2MMAIN.BAS  
    ...エディタ本体。YS2MEDITから起動される。  

- YS2MEDIT.BIN  
    ...エディタ機械語部＋エディタ補助データ。  

    YS2MEDITで読み込まれる。  
    tniAsmでYS2MEDIT.ASMをアセンブルした物。  

- YS2MEDIT.BOF  
    ...YS2MEDIT.BINと同等の物。  

    MSX2ASMでYS2MEDIT.ASFをアセンブルした物。  
    現在は不要。  

    MSX本体でアセンブルしたい場合はこちらを使用する形になる。  
    
    こちらを使用したい場合は、  
    YS2MEDITのBLOAD"YS2MEDIT.BIN",RをBLOAD"YS2MEDIT.BOF",Rに変更するか、  
    YS2MEDIT.BOFをYS2MEDIT.BINにリネームする。  

- YS2MEDIT.ASF  
    ...機械語部分の機械語ソースファイル。  

    MSX2ASMでアセンブルする場合はこちらを使用する。  
    （tniASMでアセンブルする場合は不要）  

    アセンブル方法：
    - RUN"MSX2ASM"→自動で再起動→_ASM("YS2MEDIT")でアセンブル
    - →N,Pを聴かれたら、
    - RETURNキーで途中表示
    - Nで途中表示なし
    - Pで途中経過をプリンタ出力
    - ビルドに成功するとセーブするか聞かれるので、
    セーブするならY。セーブしないならそれ以外を入力

    アセンブルされたバイナリファイルは"YS2MEDIT.BOF"として保存される  

---
## ■ その他ファイル解説

- SRC\YSEMEDIT.ASM  
    ...YS2MEDIT.BINのソースファイル  

    tniASMでアセンブルできます。  
    アセンブルしたらYS2MEDIT.BINが出来るので  
    DSKイメージ（または実FDD）の中にコピーしてください。  

---
## ■ 変更履歴

- 2020/07/17 高速化＆潜在バグ修正＆tniASM向けソースファイルの追加

    - バグ＆高速化

        問題：

        VDPレジスタアクセスの間隔が12ステート未満だったために、
        - MSX2で環境によっては画面描画がバグる事がある。
        - MSX2+以降ではVDPアクセス時に余計な自動アクセスウェイトが入って遅くなる。

        対処：

        OUT(C),Aが11ステートなので、
        OUT (C),Aのあとに、連続してOUT命令を使わないように、間に別の処理を移動した。

        OUT命令とOUT命令の間に他の処理をするようにしたので、ターボRモードでは高速化にもなった。

        （連続アクセス間隔制限より短い連続アクセスがあると
        ターボRの高速モードでもZ80の12ステート相当のウェイトが入る為、
        OUT命令とOUT命令の間に出来るだけ他の処理をすると高速化の効果がある模様。）

    - tinASM向けのソースファイル：

        MSX2ASM向けのASFファイルはTABを使いたい箇所で空白を一個しか使ってはいけない為、非常に見づらい。

        （本来は直接編集用のファイルではなく、拡張BASICで編集するものなので）

        tniASM用のソースファイルのほうが制限が少なくて見やすいため、
        tniASM向けの記述のYS2MEDIT.ASMを用意した。

        （アセンブルもWINDOWS等で実行するため速い）


- 2020/07/16 とりあえず配布





