<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="08bb7-101">Visual Studio を開き、[**ファイル > 新しい > プロジェクト**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-101">Open Visual Studio, and select **File > New > Project**.</span></span> <span data-ttu-id="08bb7-102">[**新しいプロジェクト**] ダイアログボックスで、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="08bb7-102">In the **New Project** dialog, do the following:</span></span>

1. <span data-ttu-id="08bb7-103">**Visual C# > Windows Universal > テンプレート**を選択します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-103">Select **Templates > Visual C# > Windows Universal**.</span></span>
1. <span data-ttu-id="08bb7-104">[**空のアプリ (Universal Windows)**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-104">Select **Blank App (Universal Windows)**.</span></span>
1. <span data-ttu-id="08bb7-105">プロジェクトの名前については、「グラフを入力してください」**というチュートリアル**を行います。</span><span class="sxs-lookup"><span data-stu-id="08bb7-105">Enter **graph-tutorial** for the Name of the project.</span></span>

![Visual Studio 2017 [新しいプロジェクトの作成] ダイアログ](./images/vs-newproj-01.png)

> [!IMPORTANT]
> <span data-ttu-id="08bb7-107">これらのラボ手順で指定した Visual Studio プロジェクトに対して、まったく同じ名前を入力してください。</span><span class="sxs-lookup"><span data-stu-id="08bb7-107">Ensure that you enter the exact same name for the Visual Studio Project that is specified in these lab instructions.</span></span> <span data-ttu-id="08bb7-108">Visual Studio プロジェクト名は、コード内の名前空間の一部になります。</span><span class="sxs-lookup"><span data-stu-id="08bb7-108">The Visual Studio Project name becomes part of the namespace in the code.</span></span> <span data-ttu-id="08bb7-109">これらの手順内のコードは、この手順で指定した Visual Studio プロジェクト名に一致する名前空間によって決まります。</span><span class="sxs-lookup"><span data-stu-id="08bb7-109">The code inside these instructions depends on the namespace matching the Visual Studio Project name specified in these instructions.</span></span> <span data-ttu-id="08bb7-110">別のプロジェクト名を使用すると、プロジェクトの作成時に入力した Visual Studio プロジェクト名と一致するようにすべての名前空間を調整しない限り、コードはコンパイルされません。</span><span class="sxs-lookup"><span data-stu-id="08bb7-110">If you use a different project name the code will not compile unless you adjust all the namespaces to match the Visual Studio Project name you enter when you create the project.</span></span>

<span data-ttu-id="08bb7-111">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-111">Select **OK**.</span></span> <span data-ttu-id="08bb7-112">[**新しいユニバーサル Windows プラットフォームプロジェクト**] ダイアログで、[**最小バージョン**] が [また`Windows 10 Fall Creators Update (10.0; Build 16299)`はそれ以降] に設定されていることを確認し、[ **OK**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-112">In the **New Universal Windows Platform Project** dialog, ensure that the **Minimum version** is set to `Windows 10 Fall Creators Update (10.0; Build 16299)` or later and select **OK**.</span></span>

<span data-ttu-id="08bb7-113">に進む前に、後で使用する追加の NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="08bb7-113">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="08bb7-114">アプリ内通知とロードインジケーターの UI コントロールを追加するには、 [Microsoft Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls/)を使用します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-114">[Microsoft.Toolkit.Uwp.Ui.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls/) to add some UI controls for in-app notifications and loading indicators.</span></span>
- <span data-ttu-id="08bb7-115">Microsoft Graph によって返される情報を表示するには、「 [Microsoft Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="08bb7-115">[Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) to display the information returned by Microsoft Graph.</span></span>
- <span data-ttu-id="08bb7-116">ログインとアクセストークンの取得を処理するための、 [Microsoft Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.Graph/) 。</span><span class="sxs-lookup"><span data-stu-id="08bb7-116">[Microsoft.Toolkit.Uwp.Ui.Controls.Graph](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.Graph/) to handle login and access token retrieval.</span></span>
- <span data-ttu-id="08bb7-117">Microsoft Graph に電話をかけるための[グラフ](https://www.nuget.org/packages/Microsoft.Graph/)です。</span><span class="sxs-lookup"><span data-stu-id="08bb7-117">[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) for making calls to the Microsoft Graph.</span></span>

<span data-ttu-id="08bb7-118">[**ツール > NuGet パッケージマネージャー > パッケージマネージャーコンソール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-118">Select **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="08bb7-119">パッケージマネージャーコンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-119">In the Package Manager Console, enter the following commands.</span></span>

```Powershell
Install-Package Microsoft.Toolkit.Uwp.Ui.Controls
Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid
Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.Graph
Install-Package Microsoft.Graph
```

## <a name="design-the-app"></a><span data-ttu-id="08bb7-120">アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="08bb7-120">Design the app</span></span>

<span data-ttu-id="08bb7-121">最初に、認証状態を追跡するアプリケーションレベルの変数を追加します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-121">Start by adding an application-level variable to track authentication state.</span></span> <span data-ttu-id="08bb7-122">ソリューションエクスプローラーで、app.xaml \*\*\*\* を展開し、 **App.xaml.cs**を開きます。</span><span class="sxs-lookup"><span data-stu-id="08bb7-122">In Solution Explorer, expand **App.xaml** and open **App.xaml.cs**.</span></span> <span data-ttu-id="08bb7-123">次のプロパティを`App`クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-123">Add the following property to the `App` class.</span></span>

```cs
public bool IsAuthenticated { get; set; }
```

<span data-ttu-id="08bb7-124">次に、メインページのレイアウトを定義します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-124">Next, define the layout for the main page.</span></span> <span data-ttu-id="08bb7-125">を`MainPage.xaml`開き、内容全体を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="08bb7-125">Open `MainPage.xaml` and replace its entire contents with the following.</span></span>

```xml
<Page
    x:Class="graph_tutorial.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:graph_tutorial"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"
    xmlns:graphControls="using:Microsoft.Toolkit.Uwp.UI.Controls.Graph"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <Grid>
        <NavigationView x:Name="NavView"
            IsSettingsVisible="False"
            ItemInvoked="NavView_ItemInvoked">

            <NavigationView.Header>
                <graphControls:AadLogin x:Name="Login"
                    HorizontalAlignment="Left"
                    View="SmallProfilePhotoLeft"
                    AllowSignInAsDifferentUser="False"
                    />
            </NavigationView.Header>

            <NavigationView.MenuItems>
                <NavigationViewItem Content="Home" x:Name="Home" Tag="home">
                    <NavigationViewItem.Icon>
                        <FontIcon Glyph="&#xE10F;"/>
                    </NavigationViewItem.Icon>
                </NavigationViewItem>
                <NavigationViewItem Content="Calendar" x:Name="Calendar" Tag="calendar">
                    <NavigationViewItem.Icon>
                        <FontIcon Glyph="&#xE163;"/>
                    </NavigationViewItem.Icon>
                </NavigationViewItem>
            </NavigationView.MenuItems>

            <StackPanel>
                <controls:InAppNotification x:Name="Notification" ShowDismissButton="true" />
                <Frame x:Name="RootFrame" Margin="24, 0" />
            </StackPanel>
        </NavigationView>
    </Grid>
</Page>
```

<span data-ttu-id="08bb7-126">これにより、アプリのメインビューとして機能する、**ホーム**および**予定表**のナビゲーションリンクが含まれる基本的な[navigationview](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.navigationview)が定義されます。</span><span class="sxs-lookup"><span data-stu-id="08bb7-126">This defines a basic [NavigationView](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.navigationview) with **Home** and **Calendar** navigation links to act as the main view of the app.</span></span> <span data-ttu-id="08bb7-127">また、ビューのヘッダーに[AadLogin](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.aadlogin?view=win-comm-toolkit-dotnet-stable)コントロールも追加されます。</span><span class="sxs-lookup"><span data-stu-id="08bb7-127">It also adds an [AadLogin](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.aadlogin?view=win-comm-toolkit-dotnet-stable) control in the header of the view.</span></span> <span data-ttu-id="08bb7-128">このコントロールによって、ユーザーはサインインとサインアウトができるようになります。コントロールが完全に有効になっていない場合は、後の手順で構成します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-128">That control will allow the user to sign in and out. The control isn't fully enabled yet, you will configure it in a later exercise.</span></span>

<span data-ttu-id="08bb7-129">次に、ホームビュー用の別の XAML ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-129">Now add another XAML page for the Home view.</span></span> <span data-ttu-id="08bb7-130">ソリューションエクスプローラーで**グラフ-チュートリアル**プロジェクトを右クリックし、[**新しいアイテムの追加 >**] を選択します。[**空白のページ**] `HomePage.xaml`を選択し、[**名前**] フィールドに「」と入力して、[**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-130">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `HomePage.xaml` in the **Name** field, and select **Add**.</span></span> <span data-ttu-id="08bb7-131">ファイル内の要素の`<Grid>`内部に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-131">Add the following code inside the `<Grid>` element in the file.</span></span>

```xml
<StackPanel>
    <TextBlock FontSize="44" FontWeight="Bold" Margin="0, 12">Microsoft Graph UWP Tutorial</TextBlock>
    <TextBlock x:Name="HomePageMessage">Please sign in to continue.</TextBlock>
</StackPanel>
```

<span data-ttu-id="08bb7-132">これで、ソリューションエクスプローラーで**MainPage**を展開し`MainPage.xaml.cs`、を開きます。</span><span class="sxs-lookup"><span data-stu-id="08bb7-132">Now expand **MainPage.xaml** in Solution Explorer and open `MainPage.xaml.cs`.</span></span> <span data-ttu-id="08bb7-133">この行の`MainPage()` `this.InitializeComponent();` **後**に、次のコードをコンストラクターに追加します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-133">Add the following code to the `MainPage()` constructor **after** the `this.InitializeComponent();` line.</span></span>

```cs
// Initialize auth state to false
SetAuthState(false);

// Navigate to HomePage.xaml
RootFrame.Navigate(typeof(HomePage));
```

<span data-ttu-id="08bb7-134">アプリが初めて起動するときに、認証状態がに`false`初期化され、ホームページに移動します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-134">When the app first starts, it will initialize the authentication state to `false` and navigate to the home page.</span></span>

<span data-ttu-id="08bb7-135">認証状態を管理するため`MainPage`に、次の関数をクラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-135">Add the following function to the `MainPage` class to manage authentication state.</span></span>

```cs
private void SetAuthState(bool isAuthenticated)
{
    (App.Current as App).IsAuthenticated = isAuthenticated;

    // Toggle controls that require auth
    Calendar.IsEnabled = isAuthenticated;
}
```

<span data-ttu-id="08bb7-136">ユーザーがナビゲーションビューでアイテムを選択したときに、要求されたページを読み込むために、次のイベントハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="08bb7-136">Add the following event handler to load the requested page when the user selects an item from the navigation view.</span></span>

```cs
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

<span data-ttu-id="08bb7-137">すべての変更を保存し、 **F5**キーを押すか、[デバッグ] を選択して Visual Studio で**デバッグを開始 >** ます。</span><span class="sxs-lookup"><span data-stu-id="08bb7-137">Save all of your changes, then press **F5** or select **Debug > Start Debugging** in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="08bb7-138">ご使用のコンピューター (ARM、x64、x86) に適した構成を選択してください。</span><span class="sxs-lookup"><span data-stu-id="08bb7-138">Make sure you select the appropriate configuration for your machine (ARM, x64, x86).</span></span>

![ホーム ページのスクリーンショット](./images/create-app-01.png)
