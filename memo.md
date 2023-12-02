## はじめに


1. この本で紹介していること

1. 必要な環境

    Astroのプロジェクトの開始は、CLIを使って行います。
    まずは、node.jsのインストールが必要です。直接インストールでも大丈夫ですが、できれば、バージョン管理ができる形でのインストールがおすすめです。少し学習コストはあがりますが、node.jsのバージョンによって過去のプロジェクトでエラーが発生することもありますので、一度チャレンジしてみてください。

    バージョン管理のツールはいろいろありますが、私はVoltaを使用しています。
    こちらの記事が参考になります。

    [Node.jsのバージョン管理はVoltaに決定](https://zenn.dev/aiueda/articles/7dcecaa05d4f24)

## Astroプロジェクトをはじめる（自動CLI使用）
1. CLI（ターミナルなど）でフォルダ作成→プロジェクト作成　
    `$ mkdir astro`  // プロジェクトを格納するフォルダ作成
    `$ cd astro` // プロジェクトを作成するフォルダへ移動
    `$ npm create astro@latest` // Astro最新バージョンでプロジェクト作成
    CLIでいろいろ聞かれます。
    基本的にはまずrecommnended(推奨)を選ぶとよいです。

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

1. 開発環境でAstroサイトをスタート〜デプロイ

    SSGなどのツールを使用した開発ではLocalサーバーで開発→Localでbuildして確認（本番に近い状態）→本番へデプロイという流れをとるのが多いです。

    1. Localサーバーで開発
        `npm start` //srcフォルダの内容からサイトを表示してくれます。
        - ブラウザでlocalhost:4321へアクセスします。        
        - pages/index.astroがトップページで表示されています。少し、変更してみましょう。 →ホットリロード機能
        - 
    1. Localで本番と同じようにbuildして確認
        `npm run build` // 本番では静的サイトとして表示されますので、そのHTML、CSS、JavaScriptのファイルを作成、これをbuildといいます。
        `npm run preview` //buildしたファイルをローカルで表示確認します

1. 本番へデプロイして確認
    - 今回はVercelというホスティングサービスを仕様
    - Gitリポジトリと連携して、push、mergeすると、新しくデプロイしてくれます。

    1. リモートリポジトリを作成
    1. デプロイして確認　vercel

## フォルダ構成を確認
1. distフォルダ
    さきほどbuildしたファイルはこのフォルダに格納されています。ここには静的サイトが構築されますので、これらのファイルをサーバーにアップロードすることで、公開することもできます。
    - *サブフォルダにアップロードするときはプロジェクトルートの設定をする必要があります
1. srcフォルダ
    開発にあたってはこのフォルダの内容を編集します。
    開発サーバーではここの内容を解析して、表示しています。
1. src/pagesフォルダ
    - この中のファイルが静的サイトでいう〜〜.htmlのファイルにあたります。このフォルダは必須フォルダです。
    - ここに配置することで、それぞれのhtmlファイルが生成されます。
    - pages内のファイル名がそのままリンクになります。
        index.astro -> /
        about.astro -> /about
        service.astro -> /service

1. src/layoutsフォルダ
    -  Layoutコンポーネント
        ヘッダーとかフッターとか
        `<slot />`に各コンテンツ

1. src/componentsフォルダ
    -  部品のフォルダ
    - 部品にわけて管理する
    
1. src/stylesフォルダ

1. publicフォルダ
    - mdファイル内で使用する画像やCMSで登録した画像などはsrcフォルダに保存しませんので、ここに格納します。
    - プロジェクトから参照するときは、piublic=rootという考え方で、パス指定をします。
    - sec内のCSSファイルやJSファイルはいろいろまとめてくれたりしますので、そうしたくない場合、このフォルダにファイルを配置して参照します。
    - robots.txt, manifest.webmanifest, faviconファイルなどを配置します。
    
1. 参考

    [Project Structure](https://docs.astro.build/ja/core-concepts/project-structure/#public)

    [Layouts](https://docs.astro.build/ja/core-concepts/layouts/)

## 制作
### ベース
1. pages内のindex.astroを確認サンプルコンテンツ削除
1. 各ページのファイルを作成
    アバウト、サービス、コンタクト
    1. デフォルトで入っているコンポーネントから学ぶ

    1. interface props

        このコンポーネントに渡されるパラメータの種類を規定
    
    1. const { href, title, body } = Astro.props;
        
        コンポーネントで使用する変数に展開

### Layoutコンポーネント
1. Layoutコンポーネントについて
1. headタグのtitle,description~コードフェンスとAstro.propsで各ページのmeta情報セット
1. Layoutコンポーネントにヘッダーとフッターをを追加する
### CSSについて
1. グローバルCSSとdestyle.cssを追加（stylesフォルダ）
    Layoutコンポーネントで読み込み→すべてのファイルに適用される
1. コンポーネントのCSS
1. ヘッダーとフッターのCSSをあててみる
### トップページ｜コンテンツ  
1. 各セクションをコンポーネントで作成
1. 何度も使いそうな部品　CTA →　Footerに゙追加
1. ボタンコンポーネント
### お知らせ
1. microCMSとの接続
1. 環境変数→vercelにも必要
### お問い合わせ作ってみる
1. SSGフォーム
2. NetlifyForms
