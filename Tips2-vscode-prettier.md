# VSCodeの拡張機能だけでprettierを有効化し、コードを自動整形してくれるようにする方法

## これは何？
個人的に開発用エディターとして普段使いしているVSCode。
その設定ファイル群の例。
今回はprettierを有効化することのみを目的としている。

## 例
次の2つのファイルを`.vscode`という名前のディレクトリの配下に作成する

extensions.json
```json:extensions.json
{
  "recommendations": ["esbenp.prettier-vscode"]
}
```

settings.json
```json:settings.json
{
  // エディタの自動保存の設定
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000,

  // 保存する同時に自動整形する
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",

  // Prettierの設定
  "prettier.arrowParens": "always",
  "prettier.trailingComma": "es5",
  "prettier.tabWidth": 2,
  "prettier.semi": false,
  "prettier.singleQuote": false,
  "prettier.printWidth": 100,

  // Prettierを使うファイル種類の例
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

上記のファイル群を作成すると、以下のようなディレクトリ構成になっているハズ
```
.vscode/ 
  ├ extensions.json
　└ settings.json
```


## 解説
まず、`extensions.json`で設定しているのは、VSCodeに拡張機能がインストールされていない時に「おすすめの拡張機能」としてポップアップさせる拡張機能を指定している。
なので多分なくても問題ない。<br>
今回の場合は、`esbenp.prettier-vscode`を`settings.json`の方でデフォルトのフォーマッターとして指定しているので、VSCodeの環境を初めて整える場合でも「おすすめの拡張機能」からインストールすれば、一々マーケットプレイス見る手間が省けるので、念のため指定している。

次に、`settings.json`の設定。<br>
こっちが重要。~~最悪これだけでも良い。~~ <br>
大体、コメント文で補足できることしか書いてないが、今回はhtmlとjavascriptを自動整形することを想定した設定ファイルにしている。<br>
`files.autoSave`の辺りは無くてもいいが、個人的にデータが消し飛ぶのが怖いので設定ファイルの方でも有効化している。<br>
`editor.formatOnSave`の辺りは必須。<br>
似たような設定に`formatOnType`や`formatOnPaste`というのもあるが、前者は入力した行、後者はペーストした文字列に対して自動整形する。<br>
Prettierの設定に関しては本家で調べたり、`esbenp.prettier-vscode`の設定をVSCode側からお好みで弄るのがいいと思うが、今回は個人的に普段使っている設定を指定しておく。<br>

## メモ
正直、「これらの設定ってVSCode側で指定してあげればいいじゃん」という話もあるが、明示的に指定しておくとチーム開発時や開発環境が変わった時などに設定をすぐに確認できるため、自分のためにもこの設定ファイルは置いておくだけで意味があると思っている。<br>
...もちろん、この`.vscode`ディレクトリはワークスペースのルートに置く必要があることだけは忘れるべからず。

## 終わり
以下、蛇足。<br>

今回のTipsのテーマ的には要らない、`files.autoSave`の設定。<br>
これを知らなかった半年くらい前の話、VSCodeで作業していたある日、保存もGitでのバージョン管理もしていないファイルが唐突なPCのシャットダウンとかいう不慮の事故で3時間分消し飛んだことがあり、それ以降絶対に有効化するようにしている。<br>

個人的にはPrettierと相性のいい設定だと思っていて、多少インデントだったりが雑なコーディングをしてもすぐに整形してくれるので大助かりしている。<br>

正直、かなり便利なので、昔の自分が知っていたらと悔やむ反面、知っていたら便利すぎてコーディング規約とか考えることが無かったと思うので、ある程度コーディングに慣れてきて、チーム開発時のコードの統一性について考え始めてから触れるのがいいんじゃないかと思ったり。



