<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="f3e54-101">このセクションでは、新しい UWP アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-101">In this section you'll create a new UWP app.</span></span>

1. <span data-ttu-id="f3e54-102">Visual Studio を開き、**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-102">Open Visual Studio, and select **Create a new project**.</span></span> <span data-ttu-id="f3e54-103">C# を使用する [**空のアプリ (Universal Windows)** ] オプションを選択し、[**次へ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-103">Choose the **Blank App (Universal Windows)** option that uses C#, then select **Next**.</span></span>

    ![Visual Studio 2019 [新しいプロジェクトの作成] ダイアログ](./images/vs-create-new-project.png)

1. <span data-ttu-id="f3e54-105">[**新しいプロジェクトの構成**] ダイアログで、 `GraphTutorial` [**プロジェクト名**] フィールドにと入力し、[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-105">In the **Configure your new project** dialog, enter `GraphTutorial` in the **Project name** field and select **Create**.</span></span>

    ![Visual Studio 2019 [新しいプロジェクトの構成] ダイアログ](./images/vs-configure-new-project.png)

    > [!IMPORTANT]
    > <span data-ttu-id="f3e54-107">これらのラボ手順で指定した Visual Studio プロジェクトに対して、まったく同じ名前を入力してください。</span><span class="sxs-lookup"><span data-stu-id="f3e54-107">Ensure that you enter the exact same name for the Visual Studio Project that is specified in these lab instructions.</span></span> <span data-ttu-id="f3e54-108">Visual Studio プロジェクトの名前が、コードでの名前空間の一部になります。</span><span class="sxs-lookup"><span data-stu-id="f3e54-108">The Visual Studio Project name becomes part of the namespace in the code.</span></span> <span data-ttu-id="f3e54-109">この手順のコードは、この手順で指定した Visual Studio プロジェクト名に一致する名前空間に応じて異なります。</span><span class="sxs-lookup"><span data-stu-id="f3e54-109">The code inside these instructions depends on the namespace matching the Visual Studio Project name specified in these instructions.</span></span> <span data-ttu-id="f3e54-110">異なるプロジェクト名を使用する場合には、Visual Studio プロジェクト作成時に入力したプロジェクト名に一致するようにすべての名前空間を調整しないと、コードがコンパイルされません。</span><span class="sxs-lookup"><span data-stu-id="f3e54-110">If you use a different project name the code will not compile unless you adjust all the namespaces to match the Visual Studio Project name you enter when you create the project.</span></span>

1. <span data-ttu-id="f3e54-111">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-111">Select **OK**.</span></span> <span data-ttu-id="f3e54-112">[**新しいユニバーサル Windows プラットフォームプロジェクト**] ダイアログで、[**最小バージョン**] が [また`Windows 10, Version 1809 (10.0; Build 17763)`はそれ以降] に設定されていることを確認し、[ **OK**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-112">In the **New Universal Windows Platform Project** dialog, ensure that the **Minimum version** is set to `Windows 10, Version 1809 (10.0; Build 17763)` or later and select **OK**.</span></span>

## <a name="install-nuget-packages"></a><span data-ttu-id="f3e54-113">NuGet パッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="f3e54-113">Install NuGet packages</span></span>

<span data-ttu-id="f3e54-114">に進む前に、後で使用する追加の NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="f3e54-114">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="f3e54-115">アプリ内通知とロードインジケーターの UI コントロールを追加するには、 [Microsoft Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls/)を使用します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-115">[Microsoft.Toolkit.Uwp.Ui.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls/) to add some UI controls for in-app notifications and loading indicators.</span></span>
- <span data-ttu-id="f3e54-116">Microsoft Graph によって返される情報を表示するには、「 [Microsoft Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f3e54-116">[Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) to display the information returned by Microsoft Graph.</span></span>
- <span data-ttu-id="f3e54-117">ログインとアクセストークンの取得を処理するための、 [Microsoft Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) 。</span><span class="sxs-lookup"><span data-stu-id="f3e54-117">[Microsoft.Toolkit.Graph.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) to handle login and access token retrieval.</span></span>

1. <span data-ttu-id="f3e54-118">**[ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー コンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-118">Select **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="f3e54-119">パッケージ マネージャー コンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-119">In the Package Manager Console, enter the following commands.</span></span>

    ```powershell
    Install-Package Microsoft.Toolkit.Uwp.Ui.Controls -Version 6.0.0
    Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid -Version 6.0.0
    Install-Package Microsoft.Toolkit.Graph.Controls -IncludePrerelease
    ```

## <a name="design-the-app"></a><span data-ttu-id="f3e54-120">アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="f3e54-120">Design the app</span></span>

<span data-ttu-id="f3e54-121">このセクションでは、アプリの UI を作成します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-121">In this section you'll create the UI for the app.</span></span>

1. <span data-ttu-id="f3e54-122">最初に、認証状態を追跡するアプリケーションレベルの変数を追加します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-122">Start by adding an application-level variable to track authentication state.</span></span> <span data-ttu-id="f3e54-123">ソリューションエクスプローラーで **、app.xaml を展開し**、 **App.xaml.cs**を開きます。</span><span class="sxs-lookup"><span data-stu-id="f3e54-123">In Solution Explorer, expand **App.xaml** and open **App.xaml.cs**.</span></span> <span data-ttu-id="f3e54-124">次のプロパティを `App` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-124">Add the following property to the `App` class.</span></span>

    ```csharp
    public bool IsAuthenticated { get; set; }
    ```

1. <span data-ttu-id="f3e54-125">メインページのレイアウトを定義します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-125">Define the layout for the main page.</span></span> <span data-ttu-id="f3e54-126">を`MainPage.xaml`開き、内容全体を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f3e54-126">Open `MainPage.xaml` and replace its entire contents with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/MainPage.xaml" id="MainPageXamlSnippet":::

    <span data-ttu-id="f3e54-127">これにより、アプリのメインビューとして機能する、**ホーム**および**予定表**のナビゲーションリンクが含まれる基本的な[navigationview](/uwp/api/windows.ui.xaml.controls.navigationview)が定義されます。</span><span class="sxs-lookup"><span data-stu-id="f3e54-127">This defines a basic [NavigationView](/uwp/api/windows.ui.xaml.controls.navigationview) with **Home** and **Calendar** navigation links to act as the main view of the app.</span></span> <span data-ttu-id="f3e54-128">また、ビューのヘッダーに[Loginbutton](https://github.com/windows-toolkit/Graph-Controls)コントロールも追加します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-128">It also adds a [LoginButton](https://github.com/windows-toolkit/Graph-Controls) control in the header of the view.</span></span> <span data-ttu-id="f3e54-129">このコントロールによって、ユーザーはサインインとサインアウトができるようになります。コントロールが完全に有効になっていない場合は、後の手順で構成します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-129">That control will allow the user to sign in and out. The control isn't fully enabled yet, you will configure it in a later exercise.</span></span>

1. <span data-ttu-id="f3e54-130">ソリューションエクスプローラーで**グラフ-チュートリアル**プロジェクトを右クリックし、[**新しいアイテムの追加 >**] を選択します。[**空白のページ**] `HomePage.xaml`を選択し、[**名前**] フィールドに「」と入力して、[**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-130">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `HomePage.xaml` in the **Name** field, and select **Add**.</span></span> <span data-ttu-id="f3e54-131">ファイル内の`<Grid>`既存の要素を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f3e54-131">Replace the existing `<Grid>` element in the file with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/HomePage.xaml" id="HomePageGridSnippet" highlight="2-5":::

1. <span data-ttu-id="f3e54-132">ソリューションエクスプローラーで**MainPage**を展開し、を`MainPage.xaml.cs`開きます。</span><span class="sxs-lookup"><span data-stu-id="f3e54-132">Expand **MainPage.xaml** in Solution Explorer and open `MainPage.xaml.cs`.</span></span> <span data-ttu-id="f3e54-133">認証状態を管理するため`MainPage`に、次の関数をクラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-133">Add the following function to the `MainPage` class to manage authentication state.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="SetAuthStateSnippet":::

1. <span data-ttu-id="f3e54-134">この行の`MainPage()` `this.InitializeComponent();` **後**に、次のコードをコンストラクターに追加します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-134">Add the following code to the `MainPage()` constructor **after** the `this.InitializeComponent();` line.</span></span>

    ```csharp
    // Initialize auth state to false
    SetAuthState(false);

    // Configure MSAL provider
    // TEMPORARY
    MsalProvider.ClientId = "11111111-1111-1111-1111-111111111111";

    // Navigate to HomePage.xaml
    RootFrame.Navigate(typeof(HomePage));
    ```

    <span data-ttu-id="f3e54-135">アプリが初めて起動するときに、認証状態がに`false`初期化され、ホームページに移動します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-135">When the app first starts, it will initialize the authentication state to `false` and navigate to the home page.</span></span>

1. <span data-ttu-id="f3e54-136">ユーザーがナビゲーションビューでアイテムを選択したときに、要求されたページを読み込むために、次のイベントハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="f3e54-136">Add the following event handler to load the requested page when the user selects an item from the navigation view.</span></span>

    ```csharp
    private void NavView_ItemInvoked(NavigationView sender, NavigationViewItemInvokedEventArgs args)
    {
        var invokedItem = args.InvokedItem as string;

        switch (invokedItem.ToLower())
        {
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

1. <span data-ttu-id="f3e54-137">すべての変更を保存し、 **F5**キーを押すか、[デバッグ] を選択して Visual Studio で**デバッグを開始 >** ます。</span><span class="sxs-lookup"><span data-stu-id="f3e54-137">Save all of your changes, then press **F5** or select **Debug > Start Debugging** in Visual Studio.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3e54-138">ご使用のコンピューター (ARM、x64、x86) に適した構成を選択してください。</span><span class="sxs-lookup"><span data-stu-id="f3e54-138">Make sure you select the appropriate configuration for your machine (ARM, x64, x86).</span></span>

    ![ホーム ページのスクリーンショット](./images/create-app-01.png)
