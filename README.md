BXpdfcrypt パッケージバンドル
=============================

LaTeX：dvipdfmx 用の暗号化設定を文書中で行う

### 前提環境

  * フォーマット： LaTeX
  * エンジン： DVI 出力に限る
  * DVIウェア： dvipdfmx（20110311 版以降）
  * 依存パッケージ：
      - atbegshi（`everypage`指定時）

### インストール

  - `*.sty` → $TEXMF/tex/latex/BXpdfcrypt

### ライセンス

本パッケージは MIT ライセンスの下で配布される。


bxpdfcrypt パッケージ
---------------------

### パッケージ読込

設定内容をオプションに記述して `\usepackage` で読み込む。

    \usepackage[<オプション>,...]{bxpdfcrypt}

※読込時に全ての設定を行うので、ユーザ命令は存在しない。

許可設定以外のオプション。

  * `user=<パスワード>`  
    `userfile=<ファイル名>`  
    `userfile`：
      ユーザパスワードを設定する。`user` はパスワード文字列そのものを設定
      できるが、LaTeX の特殊文字（`\` など）は使えない。一方 `userfile` は
      パスワードが記述された(1 行だけの)テキストファイルの名前を指定し、
      こちらは任意の ASCII 文字を含めることができる。単に `userfile` だけ
      指定した場合は user.txt をファイル名とする。ユーザパスワードの
      既定値は空文字列である。
  * `owner=<パスワード>`  
    `ownerfile=<ファイル名>`  
    `ownerfile`：
      所有者パスワードを指定する。詳細はユーザパスワードのオプションと
      同様。単に `ownerfile` だけの指定は owner.txt をファイル名とする。
      所有者パスワードの既定値は空文字列である。
  * `length=<値>`：
      暗号鍵のビット長。値は 40 か 128 に限る。
  * `perm=<値>`：
      許可フラグの値を直接指定する。

許可設定のオプションは、基本的に qpdf の体系に準じている（qpdf は
Adobe Acrobat での設定方式を基にしているらしい）。なお、全ての
オプションについて、`<値>` は省略が可能で、その場合は `true` が指定
されたのと同じになる。許可設定の既定値は「何も許可しない」である。
(⁎) 印の設定は `length` が 128 の時にのみ使用できる。

  * `print=<値>`：
      印刷に関する許可の設定。有効な値は次の通り。
      - `false` 又は `none`: 許可しない。
      - `low`(⁎): 低品位の印刷のみ許可。
      - `true` 又は `full`: 高品位の印刷を許可。
  * `modify=<値>`：
      文書の改変に関する許可の設定。有効な値は次の通り。
      - `false` 又は `none`: 許可しない。
      - `assembly`(⁎): 内容無改変の組換操作のみ許可。
      - `form`(⁎): 前項に加え、既存フォームへの書込を許可。
      - `annotate`: 前項に加え、注釈の編集を許可。
      - `true` 又は `all`: 全て許可する。
  * `extract=<値>`：
      情報の抽出に関する許可の設定。有効な値は次の通り。
      - `false` 又は `none`: 許可しない。
      - `accessibility`(⁎): ユーザ補助を目的とする抽出のみ許可する。
      - `true` 又は `all`: 全て許可する。

さらに、以下のものが qpdf との互換のために存在する。

  * `annotate=true`  
    `annotate`：
      `modify` が `annotate` より下のレベル（`form`, `assembly`, `false`）
      の場合は `annotate` に変更する。  
      ※ `length=40` の場合も含め、`modify=true` は実質的に `annotate`
      も有効にする。この点は qpdf と異なる。
  * `accessibility=true`(⁎)  
    `accessibility`(⁎)  
      `extract` が `false` の場合は `accessibility` に変更する。  
      ※ `extract=true` は実質的に `accessibility` も有効にする。この点は
      qpdf と異なる。

### 注意事項

  - パスワードには空白文字を含むことが可能だが、先頭や末尾に含ませる
    ことはできない。また、パスワードに使えるのは ASCII 文字のみであり
    pLaTeX であっても和文文字は使えない。


更新履歴
--------

  * Version 0.2  ‹2020/09/27›
      - LaTeX カーネル 2020/10/01 版への対応。
  * Version 0.1  ‹2011/03/20›
      - 最初の公開版。

--------------------
Takayuki YATO (aka. "ZR")  
https://github.com/zr-tex8r
