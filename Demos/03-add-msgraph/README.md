# <a name="how-to-run-the-completed-project"></a>完了したプロジェクトを実行する方法

## <a name="prerequisites"></a>前提条件

このフォルダーで完了したプロジェクトを実行するには、次のものが必要です。

- 開発用コンピューターにインストールされている[Visual Studio](https://visualstudio.microsoft.com/vs/) 。 Visual Studio を持っていない場合は、「ダウンロードオプション」の前のリンクにアクセスしてください。 (**注:** このチュートリアルは、Visual Studio 2017 バージョン15.81 で記述されています。 このガイドの手順は、他のバージョンでは動作しますが、テストされていません。)
- Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または microsoft 職場または学校のアカウントのいずれか。

Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。

- [新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。
- [office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。

## <a name="register-a-native-application-with-the-application-registration-portal"></a>ネイティブアプリケーションをアプリケーション登録ポータルに登録する

1. ブラウザーを開き、[アプリケーション登録ポータル](https://apps.dev.microsoft.com)に移動して、**個人アカウント**(別名: Microsoft アカウント) または**職場または学校のアカウント**を使用してログインします。

1. ページの上部にある [**アプリの追加**] を選択します。

    > **注:** ページに [**アプリの追加**] ボタンが複数表示されている場合は、[収束した**アプリ**] リストに対応するボタンを選択します。

1. [**アプリケーションの登録**] ページで、[**アプリケーション名**] を「 **UWP Graph チュートリアル**」に設定し、[**作成**] を選択します。

    ![アプリ登録ポータル web サイトで新しいアプリを作成するスクリーンショット](../../../Images/arp-create-app-01.png)

1. [ **UWP Graph のチュートリアル登録**] ページの [**プロパティ**] セクションで、後で必要になるように**アプリケーション Id**をコピーします。

    ![新しく作成されたアプリケーションの ID のスクリーンショット](../../../Images/arp-create-app-02.png)

1. [**プラットフォーム**] セクションまで下にスクロールします。

    1. [**プラットフォームの追加**] を選択します。
    1. [**プラットフォームの追加**] ダイアログで、[**ネイティブアプリケーション**] を選択します。

        ![アプリのプラットフォームを作成するスクリーンショット](../../../Images/arp-create-app-03.png)

1. ページの一番下までスクロールして、[**保存**] を選択します。

## <a name="configure-the-sample"></a>サンプルを構成する

1. ファイルの`OAuth.resw.example`名前を`OAuth.resw`に変更します。
1. Visual `graph-tutorial.sln` Studio で開きます。
1. visual studio `OAuth.resw`でファイルを編集します。を`YOUR_APP_ID_HERE`アプリ登録ポータルで取得した**アプリケーション Id**に置き換えます。
1. ソリューションエクスプローラーで、**グラフチュートリアル**ソリューションを右クリックして、[ **NuGet パッケージの復元**] を選択します。

## <a name="run-the-sample"></a>サンプルを実行する

Visual Studio で、 **F5**キーを押すか、デバッグ > を選択して**デバッグを開始**します。