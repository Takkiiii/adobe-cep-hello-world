# Adobe CEP Sample

Adobe CEP Extension開発についてのレポジトリ

## 開発ツール

Visual Studio Code 1.30.0

## あると便利な Visual Studio Code 拡張

1. [ExtendScript](https://marketplace.visualstudio.com/items?itemName=hennamann.jsx)
2. [CC Extension Builder](https://marketplace.visualstudio.com/items?itemName=hennamann.jsx)
3. [Adobe Script Runner](https://marketplace.visualstudio.com/items?itemName=renderTom.adobe-script-runner)

## Getting Started

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
