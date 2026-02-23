# Claude 拡張機能 導入ガイド for Windows (2026年2月版)

このドキュメントは、Windows 11＋WSL 2 (Ubuntu)環境でVisual Studio Code (VS Code) を使用して、Anthropic社のAI「Claude」をコーディングに活用するための環境構築手順をまとめたものです。

※「Claude」の読み方は、クラウド、もしくはクロード。

## 導入の全体像

- [ ] 前提条件の確認
- [ ] Claude拡張機能のインストール
- [ ] 拡張機能へのAPIキー設定
- [ ] 動作確認

## 前提条件

本手順を開始する前に、お使いの環境が以下の条件を満たしていることを確認してください。

- [ ] OS: Windows 11
- [ ] Visual Studio Code: インストール済み
- [ ] [Anthropic アカウント](https://console.anthropic.com/): アカウントが作成済みであること
- [ ] [Anthropic APIキー](https://console.anthropic.com/settings/keys): APIキーが取得済みであること

## 導入手順

### 1. Anthropic アカウントの取得からClaude Pro（月額20ドル）への契約

1. [チャット版サイト](https://claude.ai/)  に、先ほどConsole Dashboardに進んだ時のアカウントでアクセス。
2. 左下の設定より「プランをアップグレード」を選ぶ。
3. Proについて、「月額」にした上で「プロプランを取得」。
4. 個人情報・決済情報を登録。
5. [Anthropic アカウント](https://console.anthropic.com/)に事前に紐づけたGoogleアカウントでログインすると、Individual（個人）かOrganization（組織）か聞かれるので、私（プライベートプロジェクト）の場合は「個人」を選択。
6. Dashboard画面に進む。

### 2. WSL 2におけるNode環境適用

Ubuntuターミナル上で実施。

Ubuntu標準のaptで入れるNode.jsはバージョンが古すぎることが多く、Claude Codeが正常に動かない可能性が高いので、nvm (Node Version Manager) を使ってNode.jsを導入。

1. `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash` を実行し、一度Ubuntuのウィンドウ（ターミナル）を完全に閉じて、もう一度開き直す。
2. `nvm install --lts`
3. `node -v`および`npm -v`よりそれぞれのソフトが入ったことを確認。

### 3. Claude Codeインストール

引き続きUbuntuターミナル上で実施。

1. `npm install -g @anthropic-ai/claude-code`実行後、`claude --version`でインストール確認。
2. Visual Studio Codeより、F1キーを押して`WSL: Connect to WSL`を選択します。
3. Visual Studio Codeの開きなおしが起こり、ウィンドウ左下が「WSL: Ubuntu」という表示になれば成功。

### 4. 作業フォルダーの用意

1. 作業フォルダーは、Ubuntu側に用意する。
2. Windows側では100個のファイルをスキャンするのに「10秒」かかる場合でも、Ubuntu側なら同じ作業が「0.5秒」で完了する。
3. Ubuntuのターミナルで`explorer.exe .`を実行し、エクスプローラーを開いて、「クィックアクセス」にピン止め。
4. Visual Studio Codeをそのフォルダーで開く`code .`
5. Visual Studio Codeのターミナルで`claude login`を実行。

### 5. Claude login

1. `Choose the text style that looks best with your terminal To change this later, run /theme`では、`1. Dark mode`を選択。
2. `Claude Code can be used with your Claude subscription or billed based on API usage through your Console account.`がでるので、まず`1. Claude account with subscription · Pro, Max, Team, or Enterprise`を選ぶ。
3. URLが出力されるのでアクセス（Ctrl＋クリック）。「OAuthリクエストが失敗しました」が出る場合はしばらく待って再トライ。
4. 「Claude CodeさんがClaude chat accountのへの接続を希望しています」とのことなので「承認する」
5. 「Authentication Code | Paste this into Claude Code:～」と出るので、Visual studio Codeに戻って貼り付けしてEnter。

### 6. 初期の動作

1. `You should always review Claude's responses, especially when running code.``Due to prompt injection risks, only use it with code you trust`においては、「セキュリティ上の注意（Security notes）」なので、目を通したうえで「Enter」で次に進む。
2. 次に最後の確認として`Quick safety check: Is this a project you created or one you trust? (Like your own code, a well-known open source project, or work from your team). If not, take a moment to review what's in this folder first.`（今開いているフォルダーを、クラウドコードが自由に読み書き・実行しても大丈夫ですか？）聞いてきている、自分で作ったフォルダーを見ているはずなので、`1. Yes, I trust this folder`を回答。
3. `✻ Welcome to Claude Code for VSCode installed extension v2.1.50`と出たらコマンド受付かいしで、利用開始となっている。Enterキーを押して説明を抜ける。

## 基本的な使い方

- **新しいチャットを開始する**:
  - `Ctrl + Shift + P` でコマンドパレットを開き、`>Claude: New Chat` を選択すると、新しいチャットタブが開きます。
  - コードの生成、リファクタリング、デバッグの相談などが可能です。

- **選択したコードについて操作する**:
  - エディターでコードを選択した状態で右クリックします。
  - コンテキストメニューから `Claude` > `Edit Code` などを選択することで、選択範囲に関する操作ができます。
