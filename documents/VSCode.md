# VSCodeの設定

## PHPデバッガー 'Xdebugger' の導入

<br>

- VS Code を使ってブレークポイントで停止、ステップ実行、変数の確認等のデバッグを行うことが可能。

1. VS Code に、拡張機能 "PHP debug(Felix Becker)" をインストール
2. VS Code を再起動し、サイドバーのディレクトリを、'.vscode' が存在するディレクトリにする。

- 以上の手順で、ブレークポイント機能が使用できる。使用するには、F5キーを押すか、サイドバーの"Run and debug" アイコンを押下し、XDebug on docker の再生ボタンを押下する。もちろん、停止したいコードの時点にブレークポイントを設定して行う。

<br>

## VSCode のおすすめ設定

<br>

- VSCodeのUIを日本語化する。英語に慣れておきたいと思っていても、まずはVSCodeに慣れるまでは日本語で使っておくとよい。後から無効化できる。
  - やり方：サイドバーの拡張機能タブ(Extension)で、Japaneseと検索して、最もインストール数が多いものをインストールする。VSCodeを再起動すると、日本語化する。

- 自動保存を有効にして、入力内容が即座に保存されるようにする。
  - やり方：「設定」で Files: Auto Save という項目を afterDelay に設定する。

- スペースを薄く表示して、スペースがいくつあるか、半角スペースか全角スペースなのかということを可視化する。
  - やり方：「設定」でEditor: Render Whitspace という項目を all に設定する

- 括弧色付け機能を有効化する。括弧の入れ子構造の時に、その範囲が分かりやすくなる。
  - やり方：https://dev.classmethod.jp/articles/replace-bracket-pair-colorizer-2-to-vscode/

<br>

- 拡張機能をインストールする。以下のコマンドでインストールできる。
  - `code --install-extension bmewburn.vscode-intelephense-client`
  - `code --install-extension donjayamanne.githistory`
  - `code --install-extension MehediDracula.php-namespace-resolver`
  - `code --install-extension mhutchie.git-graph`
  - `code --install-extension oderwat.indent-rainbow`
  - `code --install-extension onecentlin.laravel-blade`
  - `code --install-extension xdebug.php-debug`
  - `code --install-extension xdebug.php-pack`
  - `code --install-extension zobo.php-intellisense`

- また、以下のコマンドで現在インストールされている拡張機能を確認できる。
  - `code --list-extensions`

<br>

- プログラミング用フォント「Ricty Dimished」をVS Code上のフォントにする（Windowsの手順）

  1. 以下のサイトにて、「RictyDiminished-Regular.ttf」をダウンロードし、実行。  
  - https://github.com/edihbrandon/RictyDiminished

  2. 1でダウンロードした「RictyDiminished-Regular.ttf」を実行して、インストール。

  3. VS Code を開き、設定を見る。「Editor: Font Family」の項目を、「'Ricty Diminished'」と入力。保存して、VS Code を再起動すれば終了。

<br>

## VSCode内で使えるショートカットキー

### 
