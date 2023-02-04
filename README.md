# お手軽uplatexテンプレートと、wxmaxima

uplatexを使い始めたはよいが、tex関係の情報がさんざん散らばっていて

エラーが出まくっていたので、落ち着いたところで、覚書を兼ねて記しておきます。

upLaTeXの迷える子猫だったので、まだ迷っている人のために。

tex latex platex uplatexは微妙に違うのですが、

Ubuntuで、和文で書く事もあり、新しいuplatexを使うこととします。

uplatexのインストール

    sudo apt install texlive-lang-cjk xdvik-ja evince texlive-fonts-recommended texlive-fonts-extra

参考

[Qiita:【Ubuntu上でtexをコンパイルしてpdfとして保存する】]
(https://qiita.com/ocian/items/0e679e8bf72a39ada335)

# お手軽uplatex template

uplatexを、インストールしたのは良いけれど、さて、ヘッダやら何やらの書き方が分からない時、

下記のテンプレートに書けば、大体通ります。

この、テンプレートは、\parindent = 0ptで、自動インデント抑止を、

\gtでゴシック体を指定してます。\parindent = 0ptとするのは、

バッドノウハウだと言われてますが。


これで、template.texを元に書いた、ファイルfoo.texから、

$ uplatex foo.texで、.dviファイルを生成し、

$ dvipdfm foo.dviで、.dviファイルから、.pdfに変換すると出来上がりです。

# コマンド入力を簡単にする。

下記のコードを、.bashrcに書いておくと良いでしょう。

$ tex exsample

とすると、exsample.texから、exsample.pdfを出力します。

platexは、エラーで停止したら、どうにもこうにもコントロールがきかないので、

エラーで止まるようにしています。

.bashrcを書き換えたら、

    $ source .bashrc

とすると、反映されます。

#TeXLive

function tex {

  uplatex -halt-on-error "$1".tex

  dvipdfm "$1".dvi

}


# wxmaxima

wxmaximaの出力をtexに貼り付ける時tex関数というのがあって、tex(式);等とすると、

maximaはtex風に数式を返して呉れますが、maximaの結果の出力表示は、

TeX風ですがTeXではありません。それに、wxmaximaの出力を、

右クリックして出てくるLATEX形式のテキストは、そのままでは、uplatexには使えませんでした。

予め、load("mactex-utilities.lisp")$としておいて、tex関数を使うと良いでしょう。

googleで、「mactex-utilities.lisp」として検索して下さい。

# online equation editor

オンラインの数式エディタは【HostMath.com】にあります。

