<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="c7f46-101">このセクションでは、新しい UWP アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-101">In this section you'll create a new UWP app.</span></span>

1. <span data-ttu-id="c7f46-102">Visual Studio を開き、**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-102">Open Visual Studio, and select **Create a new project**.</span></span> <span data-ttu-id="c7f46-103">C# **を使う空白のアプリ (ユニバーサル Windows)** オプションを選択し、[次へ] を選択 **します**。</span><span class="sxs-lookup"><span data-stu-id="c7f46-103">Choose the **Blank App (Universal Windows)** option that uses C#, then select **Next**.</span></span>

    ![Visual Studio 2019 で新しいプロジェクトの作成ダイアログを作成する](./images/vs-create-new-project.png)

1. <span data-ttu-id="c7f46-105">[新しい **プロジェクトの構成]** ダイアログ で、[プロジェクト名] フィールドに `GraphTutorial` **「** 作成」を選択 **します**。</span><span class="sxs-lookup"><span data-stu-id="c7f46-105">In the **Configure your new project** dialog, enter `GraphTutorial` in the **Project name** field and select **Create**.</span></span>

    ![Visual Studio 2019 の [新しいプロジェクトの構成] ダイアログ](./images/vs-configure-new-project.png)

    > [!IMPORTANT]
    > <span data-ttu-id="c7f46-107">このラボの手順で指定されているプロジェクトの名前とVisual Studio名前を入力してください。</span><span class="sxs-lookup"><span data-stu-id="c7f46-107">Ensure that you enter the exact same name for the Visual Studio Project that is specified in these lab instructions.</span></span> <span data-ttu-id="c7f46-108">Visual Studio プロジェクトの名前が、コードでの名前空間の一部になります。</span><span class="sxs-lookup"><span data-stu-id="c7f46-108">The Visual Studio Project name becomes part of the namespace in the code.</span></span> <span data-ttu-id="c7f46-109">この手順のコードは、この手順で指定した Visual Studio プロジェクト名に一致する名前空間に応じて異なります。</span><span class="sxs-lookup"><span data-stu-id="c7f46-109">The code inside these instructions depends on the namespace matching the Visual Studio Project name specified in these instructions.</span></span> <span data-ttu-id="c7f46-110">異なるプロジェクト名を使用する場合には、Visual Studio プロジェクト作成時に入力したプロジェクト名に一致するようにすべての名前空間を調整しないと、コードがコンパイルされません。</span><span class="sxs-lookup"><span data-stu-id="c7f46-110">If you use a different project name the code will not compile unless you adjust all the namespaces to match the Visual Studio Project name you enter when you create the project.</span></span>

1. <span data-ttu-id="c7f46-111">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c7f46-111">Select **OK**.</span></span> <span data-ttu-id="c7f46-112">[新しい **ユニバーサル Windows プラットフォーム プロジェクト]** ダイアログで、[最小バージョン] が設定されている以降のバージョンを確認し `Windows 10, Version 1809 (10.0; Build 17763)` **、[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-112">In the **New Universal Windows Platform Project** dialog, ensure that the **Minimum version** is set to `Windows 10, Version 1809 (10.0; Build 17763)` or later and select **OK**.</span></span>

## <a name="install-nuget-packages"></a><span data-ttu-id="c7f46-113">NuGet パッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="c7f46-113">Install NuGet packages</span></span>

<span data-ttu-id="c7f46-114">次に進む前に、後で使用する追加の NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="c7f46-114">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="c7f46-115">Microsoft Graph Toolkit返される情報を表示するための[Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid。](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/)</span><span class="sxs-lookup"><span data-stu-id="c7f46-115">[Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) to display the information returned by Microsoft Graph.</span></span>
- <span data-ttu-id="c7f46-116">[ログインとToolkit取得を処理する Microsoft.Toolkit.Graph.Controls。](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls)</span><span class="sxs-lookup"><span data-stu-id="c7f46-116">[Microsoft.Toolkit.Graph.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) to handle login and access token retrieval.</span></span>

1. <span data-ttu-id="c7f46-117">**[ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー コンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-117">Select **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="c7f46-118">パッケージ マネージャー コンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-118">In the Package Manager Console, enter the following commands.</span></span>

    ```powershell
    Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid -IncludePrerelease
    Install-Package Microsoft.Toolkit.Graph.Controls -IncludePrerelease
    ```

## <a name="design-the-app"></a><span data-ttu-id="c7f46-119">アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="c7f46-119">Design the app</span></span>

<span data-ttu-id="c7f46-120">このセクションでは、アプリの UI を作成します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-120">In this section you'll create the UI for the app.</span></span>

1. <span data-ttu-id="c7f46-121">まず、認証状態を追跡するアプリケーション レベルの変数を追加します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-121">Start by adding an application-level variable to track authentication state.</span></span> <span data-ttu-id="c7f46-122">ソリューション エクスプローラーで **App.xaml を展開し、アプリ** を **開** App.xaml.cs。</span><span class="sxs-lookup"><span data-stu-id="c7f46-122">In Solution Explorer, expand **App.xaml** and open **App.xaml.cs**.</span></span> <span data-ttu-id="c7f46-123">次のプロパティを `App` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-123">Add the following property to the `App` class.</span></span>

    ```csharp
    public bool IsAuthenticated { get; set; }
    ```

1. <span data-ttu-id="c7f46-124">メイン ページのレイアウトを定義します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-124">Define the layout for the main page.</span></span> <span data-ttu-id="c7f46-125">コンテンツ `MainPage.xaml` 全体を開き、次の内容に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="c7f46-125">Open `MainPage.xaml` and replace its entire contents with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/MainPage.xaml" id="MainPageXamlSnippet":::

    <span data-ttu-id="c7f46-126">これにより、ホーム、カレンダー、および新しいイベント ナビゲーションリンクを含む基本的な[NavigationView](/uwp/api/windows.ui.xaml.controls.navigationview)が定義され、アプリのメイン ビューとして機能します。 </span><span class="sxs-lookup"><span data-stu-id="c7f46-126">This defines a basic [NavigationView](/uwp/api/windows.ui.xaml.controls.navigationview) with **Home**, **Calendar**, and **New event** navigation links to act as the main view of the app.</span></span> <span data-ttu-id="c7f46-127">また、ビューの [ヘッダーに LoginButton](https://github.com/windows-toolkit/Graph-Controls) コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-127">It also adds a [LoginButton](https://github.com/windows-toolkit/Graph-Controls) control in the header of the view.</span></span> <span data-ttu-id="c7f46-128">このコントロールにより、ユーザーはサインインとサインアウトが可能です。コントロールはまだ完全には有効になっていませんが、後の演習で構成します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-128">That control will allow the user to sign in and out. The control isn't fully enabled yet, you will configure it in a later exercise.</span></span>

1. <span data-ttu-id="c7f46-129">ソリューション エクスプローラーで **グラフ チュートリアル プロジェクトを** 右クリックし、[新しいアイテムの追加> **を選択します**。Choose **Blank Page,** enter `HomePage.xaml` in the **Name** field, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="c7f46-129">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `HomePage.xaml` in the **Name** field, and select **Add**.</span></span> <span data-ttu-id="c7f46-130">ファイル内の既存 `<Grid>` の要素を次の要素に置き換える。</span><span class="sxs-lookup"><span data-stu-id="c7f46-130">Replace the existing `<Grid>` element in the file with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/HomePage.xaml" id="HomePageGridSnippet" highlight="2-5":::

1. <span data-ttu-id="c7f46-131">ソリューション **エクスプローラーで MainPage.xaml** を展開し、開きます `MainPage.xaml.cs` 。</span><span class="sxs-lookup"><span data-stu-id="c7f46-131">Expand **MainPage.xaml** in Solution Explorer and open `MainPage.xaml.cs`.</span></span> <span data-ttu-id="c7f46-132">次の関数をクラスに追加 `MainPage` して、認証状態を管理します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-132">Add the following function to the `MainPage` class to manage authentication state.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="SetAuthStateSnippet":::

1. <span data-ttu-id="c7f46-133">次のコードを行の後 `MainPage()` の **コンストラクターに** 追加 `this.InitializeComponent();` します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-133">Add the following code to the `MainPage()` constructor **after** the `this.InitializeComponent();` line.</span></span>

    ```csharp
    // Initialize auth state to false
    SetAuthState(false);

    // Configure MSAL provider
    // TEMPORARY
    MsalProvider.ClientId = "11111111-1111-1111-1111-111111111111";

    // Navigate to HomePage.xaml
    RootFrame.Navigate(typeof(HomePage));
    ```

    <span data-ttu-id="c7f46-134">アプリが最初に起動すると、認証状態が初期化され、ホーム ページ `false` に移動します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-134">When the app first starts, it will initialize the authentication state to `false` and navigate to the home page.</span></span>

1. <span data-ttu-id="c7f46-135">ユーザーがナビゲーション ビューからアイテムを選択するときに、要求されたページを読み込む次のイベント ハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="c7f46-135">Add the following event handler to load the requested page when the user selects an item from the navigation view.</span></span>

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

1. <span data-ttu-id="c7f46-136">すべての変更を保存し **、F5** キーを押するか、[デバッグ] を選択>デバッグを開始Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c7f46-136">Save all of your changes, then press **F5** or select **Debug > Start Debugging** in Visual Studio.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7f46-137">コンピューターに適した構成 (ARM x64、x86) を選択してください。</span><span class="sxs-lookup"><span data-stu-id="c7f46-137">Make sure you select the appropriate configuration for your machine (ARM, x64, x86).</span></span>

    ![ホーム ページのスクリーンショット](./images/create-app-01.png)
