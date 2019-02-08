# Adobe CEP Sample

Adobe CEP Extension開発についてのレポジトリ

## 開発ツール

Visual Studio Code 1.30.0

## あると便利な Visual Studio Code 拡張

1. [ExtendScript](https://marketplace.visualstudio.com/items?itemName=hennamann.jsx)
2. [CC Extension Builder](https://marketplace.visualstudio.com/items?itemName=hennamann.jsx)
3. [Adobe Script Runner](https://marketplace.visualstudio.com/items?itemName=renderTom.adobe-script-runner)

## Getting Started

※上記の拡張がインストールしている前提

1. コマンドパレットを実行
2. 「Create a New CC Extension」コマンドを見つける
3. Extension IDを入力(デフォルトは「com.example.helloworld」)
4. Extensionの名称を入力
5. どのテンプレートを利用するか選択

    a. basic

        単純な「Hello World」のよくあるテンプレート
        中身のファイルには本当に基本的なものしか記述されていない

    b topcoat

        AdobeのオープンソースCSSライブラリの名称
        CSSを導入したもの

    c spectrum

        topcoatの代わりにspectrumというCSSライブラリを用いたもの

    d theme
        カスタム

※テンプレートの作成場所はmacOSXの場合は下記である。

```
~/Library/Application Support/Adobe/CEP/extensions/
```

ここに置いてあるExtensionは、manifestで指定したアプリケーションとバージョンすべてで利用可能。

## 例(InDesign)

InDesignで使えるように、manifestファイルを修正する。 CSXSフォルダにあるmanifest.xmlを開き以下のように書き換える。

``` xml
<Host Name="IDSN" Version="10.0" />
....
```

単一バージョン表記だと、そのバージョン以降実行可能となる（この例では10.0＝CC2014以降）。動作バージョンを範囲で指定する場合は[10.0, 13.1]のように記述する。

※manifest.xmlに関しては[こちら](https://forums.adobe.com/docs/DOC-8786)を参考にすること。

### DebugModeの設定

~~コマンドパレットから `Enable CEP Debug Mode` を実行する。これでCEP Extensionをテストできる状態になる（元の状態に戻すときはDisableを実行する）。~~

Debugする時は、以下のコマンドを実行する。
```
defaults write com.adobe.CSXS.7 PlayerDebugMode 1 //ほぼCC 2017用
defaults write com.adobe.CSXS.8 PlayerDebugMode 1 //ほぼCC 2018用
defaults write com.adobe.CSXS.9 PlayerDebugMode 1 //ほぼCC 2019用
```

(VSCode上では厳しい？)


## 実行

manifestでバージョン指定したInDesignを起動し、ウィンドウメニュー＞エクステンションと開くと、先程サンプルとして作成したCEPが選べることができ、実行することができる。

## 証明書の発行

[ここ](https://github.com/Adobe-CEP/CEP-Resources)より、 `ZXPSignCmd` をダウンロードする。以下のコマンドを実行する。

```
ZXPSignCmd -selfSignedCert 国名コード 地域 組織 名前 パスワード 出力ファイルパス.p12 for osx
ZXPSignCmd.exe -selfSignedCert 国名コード 地域 組織 名前 パスワード 出力ファイルパス.p12 for win
```

ツールのコマンドは[PACKAGING AND SIGNING ADOBE EXTENSIONS TECHNICAL NOTE](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/creativesuite/pdfs/SigningTechNote_CC.pdf)を参考にすること。

## パッケージ化

以下のコマンドを実行する。

```
ZXPSignCmd -sign ソースフォルダのパス 出力ファイルパス.zxp 証明書.p12 設定した証明書のパスワード for osx
ZXPSignCmd.exe -sign ソースフォルダのパス 出力ファイルパス.zxp 証明書.p12 設定した証明書のパスワード for win
```

`.zxp` が生成される。

## ZXPをインストールする方法

ZXPをAdobe製品へインストールするには、ツールが必要となる。ExMan Command Line Toolなるものを使用する。

1. Adobe Extension Manager CCを[こちらから](https://www.adobe.com/jp/exchange/em_download/)ダウンロードする。
2. Adobe Extension Manager CCをインストールする。
3. ExManCmdが配置されていのフォルダへ移動する。
    * Windowsの場合:C:\Program Files\Adobe\Adobe Extension Manager CC\ 
    * MacOSXの場合:/Applications/Adobe Extension Manager CC/Adobe Extension Manager CC.app/Contents/MacOS/
4. コマンドラインツールを実行しインストールを開始する。
