### **機能要件**

### **1. ユーザープロフィール作成**

- ユーザーはサインアップして、名前、年齢、居住地、趣味、簡単な自己紹介などを含む詳細なプロファイルを作成できます。
- プロフィール写真をアップロードするオプションがあります。
- ユーザーが他のユーザーをフォローしたり、フォローされたりできるフォロワー＆フォローシステムがあります。

### **2. ユーザー投稿**

- ユーザーは一度投稿すると更新できない短いメッセージを投稿できます。これらのメッセージは最大 255 文字です。
- ユーザーはいつでも投稿を削除できます。
- 投稿で画像や動画などのメディアコンテンツを共有できる機能があります。
    - 動画の場合、サイズを制限し、必要に応じてバックエンドでさらに圧縮を行います。レンダリングには HTML 動画を使用できます。
- 投稿に「いいね」を付けたり、取り消したりする機能があります。
- 投稿を後で特定の日時に投稿されるようにスケジュールする機能があります。
    - スケジュールされた投稿のためには、毎分実行される Linux の cron ジョブからコマンドを実行することができます（例：* * * * * command-to-execute）。このコマンドは、現在投稿される予定のすべての投稿を取得し、投稿します（例：下書きから公開にステータスを変更する）。
- 返信で形成されるスレッドを許可します。投稿に返信すると、その投稿に対する返信のスレッドが形成されます。これらはネストされる場合があり、返信もそれ自体のスレッドになることがあります。

### **3. プライベートメッセージング**

- ユーザー間の直接コミュニケーションのためのプライベートメッセージングシステムがあります。
- すべてのプライベートメッセージは、暗号化された後にデータベースに保存され、読む際に復号されます。
    - PHP では、[暗号化](https://www.php.net/manual/en/function.openssl-encrypt.php)＆[復号化](https://www.php.net/manual/en/function.openssl-decrypt.php)に [PHP OpenSSL](https://www.php.net/manual/en/book.openssl.php) ライブラリを使用します。[OpenSSL](https://www.openssl.org/) には一般的な暗号化のためのコアライブラリが含まれています。

### **4. 通知**

- 新しい「いいね」、コメント、フォロワーに対する通知があります。
- 新しいプライベートメッセージが届いた際の通知があります。
- 通知カードがクリックされると、ユーザーはソースへ移動します。
    - 「いいね」通知は投稿へ、「コメント」通知はコメントへ、「フォロワー」通知はフォローしたフォロワーへ、「プライベートメッセージ」通知は会話へ移動します。
- 通知が閲覧された後、それは閲覧済みとマークされ、強調表示されません。

### **5. ホームページとタイムライン**

- トレンドとフォロワーの2つのタブを持つ、最新の投稿を表示するホームページタイムラインがあります。
    - トレンド: その日に最も「いいね」された投稿を降順で表示します。
    - フォロワー: フォロワーからの投稿を降順で表示します。
- タイムラインをスクロールすると、ページは自動的に次の投稿セットをロードします。デフォルトでは、一度に 20 の投稿がロードされます。

### **6. プロトタイプ用のデータシーディング**

- 複数の偽ユーザープロファイルでデータベースを自動的にシードします。各プロファイルは、ユニークなユーザー名、生成されたプロフィール写真、bio など、現実的な属性を持つ必要があります。
- 各偽ユーザーは、毎日ランダムなテキストジェネレーターを使用した内容の異なる 3 つの投稿を行うようにスケジュールされる必要があります。
- 各偽ユーザーは、毎日他のユーザーから 5つのランダムな投稿に「いいね」するようにプログラムされる必要があります。
- 各偽ユーザーは、毎日 1 つのランダムなメイン投稿に返信する必要があります。
- 各偽ユーザーは、毎日 50 人の「インフルエンサー」アカウントの中から 20 の投稿に「いいね」をします。これは、ユーザーが頻繁に人気アカウントのコンテンツに関与する一般的なソーシャルメディアの行動を模倣することを目的としています。
- 投稿、いいね、返信などのすべてのシーディング活動は、一日を通じて偽ユーザーごとに異なる時間にスケジュールされるべきです。一定の間隔で投稿に「いいね」するなど、活動が自動化されたように見えるパターンを避けてください。

### **技術要件**

### **フロントエンド**

- HTML/CSS を使用して、クリーンで直感的なインターフェースをデザインします。
- JavaScript を使用してクライアント側の計算を行い、Web API 呼び出しのために fetch を使用します。

### **バックエンド**

- PHP 8、TypeScript、Java、C# などの静的型付けを持つオブジェクト指向のバックエンド言語を使用します。高速なプロトタイピングのために PHP 8 が推奨されます。
- バックエンドは MVC アーキテクチャに従うべきです。

### **データベース**

- ユーザーデータ、投稿、相互作用、メッセージを保存するために MySQL などのリレーショナルデータベースシステムを利用します。
- 最適化されたデータ取得のために効果的なインデックスを実装します。

### **サーバ**

- コマンド実行のスケジュールを設定するために cron ジョブを実行する Linux マシンを使用します。

### **非機能要件**

### **デプロイメント**

- AWS のようなクラウドプラットフォームにアプリケーションをホストし、アクセス性と高い稼働時間を確保します。
- 効率的なコードデプロイメントとアップデートのためにデプロイメントスクリプトを開発しCI/CDを実装します。Github Webhooksを使うことでmasterブランチが更新される度デプロイメントスクリプトを実行し自動化もできます。
- 自分のドメインで SSL 証明書を使って本番環境にデプロイします。

### **パフォーマンス**

- 高速なロード時間と応答性の高いインタラクションを最適化します。
- 大量のユーザーデータと相互作用を効率的に処理します。

### **セキュリティ**

- 本番環境では、すべての接続は HTTPS を通じて行われる必要があります。
- ユーザーからの入力に対してバックエンドで検証が行われるべきです。
- 強力な暗号化方法による強固な認証、データ保護、プライバシーを確保します。
- ユーザーの適切なアクセス制御を実装します。Web アプリが提供するすべてのコントロールに適切な権限チェックを行います。
- 環境ファイルはソースコントロール（Git/GitHub など）で無視されるべきです。環境ファイルはサーバごとに管理されるべきです。これは SSH や SFTP を通じて行うことができます。

### **ソフトウェア設計**

- （要件モデリング）実装開発サイクルに入る前に、アクティビティ図、シーケンス図、ユースケース図などの図を作成して要件を把握し、要件モデリングを行います。
- （ソフトウェア実装設計）アジャイル開発を採用し、ソフトウェア設計を反復しながら、データベーステーブルの ER 図やモデルのクラス図を作成します。
- （フロントエンド設計）ビューの開発に入る前に、ワイヤーフレームやデジタルデザインを作成してフロントエンドデザインを行います。Figma、Whimsical、Google Draw などのアプリを使用してデザインできます。

### **スケーラビリティ**

- アプリケーションが単一のサーバ上でのみ実行され、垂直スケーリングのみが可能であると仮定します。つまり、ハードウェアのみを変更できます。