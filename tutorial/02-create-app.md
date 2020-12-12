<!-- markdownlint-disable MD002 MD041 -->

このセクションでは、新しい UWP アプリを作成します。

1. Visual Studio を開き、**[新しいプロジェクトの作成]** を選択します。 C# **を使う空白のアプリ (ユニバーサル Windows)** オプションを選択し、[次へ] を選択 **します**。

    ![Visual Studio 2019 で新しいプロジェクトの作成ダイアログを作成する](./images/vs-create-new-project.png)

1. [新しい **プロジェクトの構成]** ダイアログ で、[プロジェクト名] フィールドに `GraphTutorial` **「** 作成」を選択 **します**。

    ![Visual Studio 2019 の [新しいプロジェクトの構成] ダイアログ](./images/vs-configure-new-project.png)

    > [!IMPORTANT]
    > このラボの手順で指定されているプロジェクトの名前とVisual Studio名前を入力してください。 Visual Studio プロジェクトの名前が、コードでの名前空間の一部になります。 この手順のコードは、この手順で指定した Visual Studio プロジェクト名に一致する名前空間に応じて異なります。 異なるプロジェクト名を使用する場合には、Visual Studio プロジェクト作成時に入力したプロジェクト名に一致するようにすべての名前空間を調整しないと、コードがコンパイルされません。

1. **[OK]** をクリックします。 [新しい **ユニバーサル Windows プラットフォーム プロジェクト]** ダイアログで、[最小バージョン] が設定されている以降のバージョンを確認し `Windows 10, Version 1809 (10.0; Build 17763)` **、[OK]** を選択します。

## <a name="install-nuget-packages"></a>NuGet パッケージをインストールする

次に進む前に、後で使用する追加の NuGet パッケージをインストールします。

- Microsoft Graph Toolkit返される情報を表示するための[Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid。](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/)
- [ログインとToolkit取得を処理する Microsoft.Toolkit.Graph.Controls。](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls)

1. **[ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー コンソール]** を選択します。 パッケージ マネージャー コンソールで、次のコマンドを入力します。

    ```powershell
    Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid -IncludePrerelease
    Install-Package Microsoft.Toolkit.Graph.Controls -IncludePrerelease
    ```

## <a name="design-the-app"></a>アプリを設計する

このセクションでは、アプリの UI を作成します。

1. まず、認証状態を追跡するアプリケーション レベルの変数を追加します。 ソリューション エクスプローラーで **App.xaml を展開し、アプリ** を **開** App.xaml.cs。 次のプロパティを `App` クラスに追加します。

    ```csharp
    public bool IsAuthenticated { get; set; }
    ```

1. メイン ページのレイアウトを定義します。 コンテンツ `MainPage.xaml` 全体を開き、次の内容に置き換えてください。

    :::code language="xaml" source="../demo/GraphTutorial/MainPage.xaml" id="MainPageXamlSnippet":::

    これにより、ホーム、カレンダー、および新しいイベント ナビゲーションリンクを含む基本的な[NavigationView](/uwp/api/windows.ui.xaml.controls.navigationview)が定義され、アプリのメイン ビューとして機能します。  また、ビューの [ヘッダーに LoginButton](https://github.com/windows-toolkit/Graph-Controls) コントロールを追加します。 このコントロールにより、ユーザーはサインインとサインアウトが可能です。コントロールはまだ完全には有効になっていませんが、後の演習で構成します。

1. ソリューション エクスプローラーで **グラフ チュートリアル プロジェクトを** 右クリックし、[新しいアイテムの追加> **を選択します**。Choose **Blank Page,** enter `HomePage.xaml` in the **Name** field, and select **Add**. ファイル内の既存 `<Grid>` の要素を次の要素に置き換える。

    :::code language="xaml" source="../demo/GraphTutorial/HomePage.xaml" id="HomePageGridSnippet" highlight="2-5":::

1. ソリューション **エクスプローラーで MainPage.xaml** を展開し、開きます `MainPage.xaml.cs` 。 次の関数をクラスに追加 `MainPage` して、認証状態を管理します。

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="SetAuthStateSnippet":::

1. 次のコードを行の後 `MainPage()` の **コンストラクターに** 追加 `this.InitializeComponent();` します。

    ```csharp
    // Initialize auth state to false
    SetAuthState(false);

    // Configure MSAL provider
    // TEMPORARY
    MsalProvider.ClientId = "11111111-1111-1111-1111-111111111111";

    // Navigate to HomePage.xaml
    RootFrame.Navigate(typeof(HomePage));
    ```

    アプリが最初に起動すると、認証状態が初期化され、ホーム ページ `false` に移動します。

1. ユーザーがナビゲーション ビューからアイテムを選択するときに、要求されたページを読み込む次のイベント ハンドラーを追加します。

    ```csharp
    private void NavView_ItemInvoked(NavigationView sender, NavigationViewItemInvokedEventArgs args)
    {
        var invokedItem = args.InvokedItem as string;

        switch (invokedItem.ToLower())
        {
            case "new event":
                throw new NotImplementedException();
                break;
            case "calendar":
                throw new NotImplementedException();
                break;
            case "home":
            default:
                RootFrame.Navigate(typeof(HomePage));
                break;
        }
    }
    ```

1. すべての変更を保存し **、F5** キーを押するか、[デバッグ] を選択>デバッグを開始Visual Studio。

    > [!NOTE]
    > コンピューターに適した構成 (ARM x64、x86) を選択してください。

    ![ホーム ページのスクリーンショット](./images/create-app-01.png)
