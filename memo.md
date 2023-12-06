## はじめに

1. この本で紹介していること

1. 必要な環境

   Astro のプロジェクトの開始は、CLI を使って行います。
   まずは、node.js のインストールが必要です。直接インストールでも大丈夫ですが、できれば、バージョン管理ができる形でのインストールがおすすめです。少し学習コストはあがりますが、node.js のバージョンによって過去のプロジェクトでエラーが発生することもありますので、一度チャレンジしてみてください。

   バージョン管理のツールはいろいろありますが、私は Volta を使用しています。
   こちらの記事が参考になります。

   [Node.js のバージョン管理は Volta に決定](https://zenn.dev/aiueda/articles/7dcecaa05d4f24)

## Astro プロジェクトをはじめる（自動 CLI 使用）

1. CLI（ターミナルなど）でフォルダ作成 → プロジェクト作成　
   `$ mkdir astro` // プロジェクトを格納するフォルダ作成
   `$ cd astro` // プロジェクトを作成するフォルダへ移動
   `$ npm create astro@latest` // Astro 最新バージョンでプロジェクト作成
   CLI でいろいろ聞かれます。
   基本的にはまず recommnended(推奨)を選ぶとよいです。

   ```
   // プロジェクトの名前
   Where should we create your new project?
   ./astro-lesson
   //最初の状態
   How would you like to start your new project?
   ● Include sample files (recommended)
   ○ Use blog template
   ○ Empty
   //依存関係（ツール）をインストールするかどうか
   Install dependencies? (recommended)
   ● Yes  ○ No
   //TypeScriptを使うかどうか
   Do you plan to write TypeScript?
   ● Yes  ○ No
   // TypeScriptのモード
   How strict should TypeScript be?
   ● Strict (recommended)
   ○ Strictest
   ○ Relaxed
   //Git 初期化するか
   Initialize a new git repository? (optional)
   ● Yes  ○ No
   ```

1. 開発環境で Astro サイトをスタート〜デプロイ

   SSG などのツールを使用した開発では Local サーバーで開発 →Local で build して確認（本番に近い状態）→ 本番へデプロイという流れをとるのが多いです。

   1. Local サーバーで開発
      `npm start` //src フォルダの内容からサイトを表示してくれます。
      - ブラウザで localhost:4321 へアクセスします。
      - pages/index.astro がトップページで表示されています。少し、変更してみましょう。 → ホットリロード機能
      -
   1. Local で本番と同じように build して確認
      `npm run build` // 本番では静的サイトとして表示されますので、その HTML、CSS、JavaScript のファイルを作成、これを build といいます。
      `npm run preview` //build したファイルをローカルで表示確認します

1. 本番へデプロイして確認

   - 今回は Vercel というホスティングサービスを仕様
   - Git リポジトリと連携して、push、merge すると、新しくデプロイしてくれます。

   1. リモートリポジトリを作成
   1. デプロイして確認　 vercel 

## フォルダ構成を確認

1. dist フォルダ
   さきほど build したファイルはこのフォルダに格納されています。ここには静的サイトが構築されますので、これらのファイルをサーバーにアップロードすることで、公開することもできます。
   - \*サブフォルダにアップロードするときはプロジェクトルートの設定をする必要があります
1. src フォルダ
   開発にあたってはこのフォルダの内容を編集します。
   開発サーバーではここの内容を解析して、表示しています。
1. src/pages フォルダ

   - この中のファイルが静的サイトでいう〜〜.html のファイルにあたります。このフォルダは必須フォルダです。
   - ここに配置することで、それぞれの html ファイルが生成されます。
   - pages 内のファイル名がそのままリンクになります。
     index.astro -> /
     about.astro -> /about
     service.astro -> /service

1. src/layouts フォルダ

   - Layout コンポーネント
     ヘッダーとかフッターとか
     `<slot />`に各コンテンツ

1. src/components フォルダ
   - 部品のフォルダ
   - 部品にわけて管理する
1. src/styles フォルダ

1. public フォルダ
   - md ファイル内で使用する画像や CMS で登録した画像などは src フォルダに保存しませんので、ここに格納します。
   - プロジェクトから参照するときは、piublic=root という考え方で、パス指定をします。
   - sec 内の CSS ファイルや JS ファイルはいろいろまとめてくれたりしますので、そうしたくない場合、このフォルダにファイルを配置して参照します。
   - robots.txt, manifest.webmanifest, favicon ファイルなどを配置します。
1. 参考

   [Project Structure](https://docs.astro.build/ja/core-concepts/project-structure/#public)

   [Layouts](https://docs.astro.build/ja/core-concepts/layouts/)

## 制作

### ベース

1. pages 内の index.astro を確認サンプルコンテンツ削除
1. 各ページのファイルを作成　リンクの仕組みを確認
   アバウト、サービス、コンタクト

   1. デフォルトで入っているコンポーネントから学ぶ

   1. interface props

      このコンポーネントに渡されるパラメータの型を規定

   1. const { href, title, body } = Astro.props;

      コンポーネントで使用する変数に展開

### Layout コンポーネント

1. Layout コンポーネントについて
1. head タグの title,description~コードフェンスと Astro.props で各ページの meta 情報セット
1. Layout コンポーネントにヘッダーとフッターをを追加する

### CSS について

1. グローバル CSS と destyle.css を追加（styles フォルダ）
   Layout コンポーネントで読み込み → すべてのファイルに適用される
1. コンポーネントの CSS
1. ヘッダーとフッターの CSS をあててみる

### トップページ｜コンテンツ

1. 各セクションをコンポーネントで作成
1. 何度も使いそうな部品　 CTA → 　 Footer に゙追加
1. ボタンコンポーネント

### お知らせ

1.  環境変数の設定

    1. .env ファイルを追加
       サービス名：over40co
       API キー＊＊＊

       ```
       MICROCMS_SERVICE_DOMAIN=<YOUR_SERVICE> # .microcms.io は含まない値
       MICROCMS_API_KEY=<YOUR_KEY_VALUE>
       ```

1.  microcms javascript sdk をインストール
    `npm install microcms-js-sdk`

1.  おまじないをコピペしてちょっと変更
    microCMS 様のブログより
    [Astro と microCMS でつくるブログサイト](https://blog.microcms.io/astro-microcms-introduction/)

    microcms-javascript-sdk でいろいろなメソッドが定義されていて、簡単に記事を取得できます。WordPress のループで記事を取ってくるイメージです。

    ブログ記事のコードの変更点

    - 型のインポートを厳密に記述する

      ```
      //ブログ記事のこの部分を
      import { createClient, MicroCMSQueries } from "microcms-js-sdk";

      //以下の用に変更
      import { createClient } from "microcms-js-sdk";
      import type { MicroCMSQueries } from "microcms-js-sdk";
      ```

    - 受け取れているか確認
      micorcms.ts において次を記述

      ```
        const client = createClient({
        serviceDomain: import.meta.env.MICROCMS_SERVICE_DOMAIN as string,
        apiKey: import.meta.env.MICROCMS_API_KEY as string, 
        });
        
        console.log(client);  //←　ここに追加
      ```

            ターミナルに次のようなものがかえってきます

            ```
            get: [Function (anonymous)],
            getList: [Function (anonymous)],
            getListDetail: [Function (anonymous)],
            getObject: [Function (anonymous)],
            getAllContentIds: [Function (anonymous)],
            getAllContents: [Function (anonymous)],
            create: [Function (anonymous)],
            update: [Function (anonymous)],
            delete: [Function (anonymous)]
            ```

1. お知らせ一覧、詳細ページ
1. トップページに最新のお知らせセクション追加
1.  環境変数 →vercel にも設定

### お問い合わせ作ってみる

1. SSG フォーム
2. NetlifyForms
