<!-- markdownlint-disable MD002 MD041 -->

Visual Studio を開き、[ **File > New > Project**] を選択します。 [**新しいプロジェクト**] ダイアログボックスで、次の操作を行います。

1. [**テンプレート > Visual C# > Windows Universal**] を選択します。
1. [**空のアプリ (Universal Windows)**] を選択します。
1. プロジェクトの名前については、「グラフを入力してください」**というチュートリアル**を行います。

![Visual Studio 2017 [新しいプロジェクトの作成] ダイアログ](./images/vs-newproj-01.png)

> [!IMPORTANT]
> これらのラボ手順で指定した Visual Studio プロジェクトに対して、まったく同じ名前を入力してください。 Visual Studio プロジェクト名は、コード内の名前空間の一部になります。 これらの手順内のコードは、この手順で指定した Visual Studio プロジェクト名に一致する名前空間によって決まります。 別のプロジェクト名を使用すると、プロジェクトの作成時に入力した Visual Studio プロジェクト名と一致するようにすべての名前空間を調整しない限り、コードはコンパイルされません。

**[OK]** をクリックします。 [**新しいユニバーサル Windows プラットフォームプロジェクト**] ダイアログで、[**最小バージョン**] が [また`Windows 10 Fall Creators Update (10.0; Build 16299)`はそれ以降] に設定されていることを確認し、[ **OK**] を選択します。

に進む前に、後で使用する追加の NuGet パッケージをインストールします。

- アプリ内通知とロードインジケーターの ui コントロールを追加するには、 [Microsoft Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls/)を使用します。
- microsoft Graph によって返される情報を表示するには、「 [microsoft Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) 」を参照してください。
- ログインとアクセストークンの取得を処理するための、 [Microsoft Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.Graph/) 。
- microsoft graph に電話をかけるための[グラフ](https://www.nuget.org/packages/Microsoft.Graph/)です。

[**ツール > NuGet パッケージマネージャー > パッケージマネージャーコンソール**] を選択します。 パッケージマネージャーコンソールで、次のコマンドを入力します。

```Powershell
Install-Package Microsoft.Toolkit.Uwp.Ui.Controls
Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid
Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.Graph
Install-Package Microsoft.Graph
```

## <a name="design-the-app"></a>アプリを設計する

最初に、認証状態を追跡するアプリケーションレベルの変数を追加します。 ソリューションエクスプローラーで、app.xaml **** を展開し、 **App.xaml.cs**を開きます。 次のプロパティを`App`クラスに追加します。

```cs
public bool IsAuthenticated { get; set; }
```

次に、メインページのレイアウトを定義します。 を`MainPage.xaml`開き、内容全体を次のように置き換えます。

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

これにより、アプリのメインビューとして機能する、**ホーム**および**予定表**のナビゲーションリンクが含まれる基本的な[navigationview](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.navigationview)が定義されます。 また、ビューのヘッダーに[AadLogin](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.aadlogin?view=win-comm-toolkit-dotnet-stable)コントロールも追加されます。 このコントロールによって、ユーザーはサインインとサインアウトができるようになります。コントロールが完全に有効になっていない場合は、後の手順で構成します。

次に、ホームビュー用の別の XAML ページを追加します。 ソリューションエクスプローラーで**グラフのチュートリアル**プロジェクトを右クリックし、[ **Add > New Item...**.] を選択します。[**空白のページ**] `HomePage.xaml`を選択し、[**名前**] フィールドにと入力して、[**追加**] を選択します。 ファイル内の要素の`<Grid>`内部に次のコードを追加します。

```xml
<StackPanel>
    <TextBlock FontSize="44" FontWeight="Bold" Margin="0, 12">Microsoft Graph UWP Tutorial</TextBlock>
    <TextBlock x:Name="HomePageMessage">Please sign in to continue.</TextBlock>
</StackPanel>
```

これで、ソリューションエクスプローラーで**MainPage**を展開し`MainPage.xaml.cs`、を開きます。 この行の`MainPage()` `this.InitializeComponent();` **後**に、次のコードをコンストラクターに追加します。

```cs
// Initialize auth state to false
SetAuthState(false);

// Navigate to HomePage.xaml
RootFrame.Navigate(typeof(HomePage));
```

アプリが初めて起動するときに、認証状態がに`false`初期化され、ホームページに移動します。

認証状態を管理するため`MainPage`に、次の関数をクラスに追加します。

```cs
private void SetAuthState(bool isAuthenticated)
{
    (App.Current as App).IsAuthenticated = isAuthenticated;

    // Toggle controls that require auth
    Calendar.IsEnabled = isAuthenticated;
}
```

ユーザーがナビゲーションビューでアイテムを選択したときに、要求されたページを読み込むために、次のイベントハンドラーを追加します。

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

すべての変更を保存し、 **F5**キーを押すか、[**デバッグ >** ] [Visual Studio でデバッグを開始] を選択します。

> [!NOTE]
> ご使用のコンピューター (ARM、x64、x86) に適した構成を選択してください。

![ホーム ページのスクリーンショット](./images/create-app-01.png)
