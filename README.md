# Getting started with KVS
プロジェクト演習（データの可視化）では、可視化ライブラリKVSを使って可視化プログラムを開発します。ここでは、演習用コンピュータにKVSを導入する方法と、簡単な使い方を説明します。KVSは以下のリポジトリで公開されています。

* https://github.com/naohisas/KVS/

## KVSの取得
gitコマンドを使って、以下の手順でKVSをローカルPC環境にコピー（クローン）してください。ここでは、ホームディレクトリ直下に作成した「Project」という名前のディレクトリにコピーを作成することを想定して説明します。

```
$ cd ~
$ cd Project
$ git clone https://github.com/naohisas/KVS.git
```

## 1. コンパイル
KVSのコンパイルを行う前に、必要となる環境変数の設定を行います。まず、KVSをインストールするためのディレクトリを準備します。ここでは、ホームディレクトリ直下に「local」という名前のディレクトリを作成し、そこにインストールすることにします。KVSをインストールすると、localディレクトリ以下に「kvs」というディレクトリが作成され、そこに必要なファイルがコピーされることになります。

```
$ cd ~
$ mkdir local
```

次に、環境変数KVS_DIRとPATHを設定します。環境変数KVS_DIRには、KVSのインストールターゲットとなるディレクトリを指定します。ここでは、上で作成した「\~/local/kvs」を指定します。さらに、KVS用コンパイルコマンド（kvsmake）や簡易可視化コマンド（kvsview）などのいくつかKVSコマンドを使うために、環境変数PATHに「$KVS_DIR/bin」を追加します。シェルにBashを使っている場合は、「\~/.bash_profile」または「\~/.bashrc」に以下の設定を追加してください。もし、これらのファイルがない場合は、「\~/.bash_profile」を作成し、以下を追記してください。

```
export KVS_DIR=~/local/kvs
export PATH=$KVS_DIR/bin:$PATH
```

環境変数の追記ができれば、以下のコマンドを実行し、現在開いているターミナル上でそれらを有効にしてください。次回ターミナルを開くときには、この操作は必要ありません。

```
$ source ~/.bash_profile
または
$ source ~/.bashrc
```

環境変数の設定が終われば、クローンして作成されたKVSというディレクトリに移動し、makeコマンドを使って以下のようにコンパイルをします。

```
$ cd KVS
$ make
```

KVSの更新などで、再コンパイルが必要となった場合には、以下のように再度コンパイルすることができます。

```
$ make rebuild
```

コンパイルしたファイルを削除するときには、以下のようなコマンドを実行します。

```
$ make clean
```

以下のようにして、デバッグオプションを有効にしてコンパイルすることも可能です。

```
$ make DEBUG=1
```

## 2. インストール
コンパイルが正常に完了すれば、以下のコマンドでKVSをインストールします。このコマンドを実行することで、ライブラリファイルなどが環境変数KVS_PATHで指定したディレクトリにコピーされます。

```
$ make install
```

アンインストールするときは、以下のコマンドを実行します。

```
$ make uinstall
```

## 3. 動作確認
正常にKVSがインストールされたかどうか確認します。ここでは、KVSのインストール後に利用可能になるコマンドを利用し、KVSが利用可能な状態であるか確認します。

### 3.1 バージョンの確認
kvscheckコマンドを利用してインストールされたKVSのバージョンを確認します。ターミナル上で、以下のように入力し、表示されるバージョンを確認してください。

```
$ kvscheck -version
KVS version : 2.9.0
```

### 3.2 テストデータの表示
kvsviewコマンドを利用してテストデータの表示を行います。まず、gitコマンドを使ってテストデータを取得します。

```
$ cd ~
$ cd Project
$ git clone https://github.com/naohisas/KVS.data.git
```

テストデータの取得が完了した後、以下のコマンドを実行しロブスターデータの等値面を可視化することができます。

```
$ kvsview -Isosurface KVS.data/lobster.fld
```

### 3.3 サンプルプログラムのコンパイルと実行
KVSソースコードの中にいくつかのサンプルプログラムが保存されています。まず、以下の手順でサンプルプログラムが保存されたディレクトリ（~/Project/Example）まで移動してください。

```
$ cd ~/Project/KVS/Example/
```

このディレクトリの下に、多くのサンプルプログラムが保存されています。ここでは、三角形を表示するサンプルプログラムを使って、コンパイルと実行の方法について確認します。以下の手順で該当のディレクトリまで移動します。

```
$ cd SupportGLUT/SimpleTriangle
```

KVSプログラムをコンパイルするときは「kvsmake」というコマンドを利用します。以下の手順でコンパイルをします。オプション「-G」は、メイクファイルを作成するためのオプションです。

```
$ kvsmake -G
$ kvsmake
```

コンパイルが正常に終了すると、以下のようにしてプログラムを実行することができます。コンパイル時に「-G」オプションを指定すると、ディレクトリ名と同じ実行ファイルが生成されます。

```
$ ./SimpleTriangle
```

## その他の情報
1. [KVSプログラミング](https://github.com/vizlab-kobe-lecture/GettingStartedWithKVS/wiki)
1. [入門KVS](https://github.com/naohisas/KVS/wiki/GettingStartedWithKVS)
1. [KVS: A simple and effective framework for scientific visualization](https://www.jstage.jst.go.jp/article/jasse/2/1/2_76/_article)
