<!-- markdownlint-disable MD002 MD041 -->

この演習では、Azure AD での認証をサポートするために、前の手順で作成したアプリケーションを拡張します。 これは、Microsoft Graph を呼び出すために必要な OAuth アクセストークンを取得するために必要です。 この手順では、 [AadLogin](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.aadlogin?view=win-comm-toolkit-dotnet-stable)コントロールを[Windows コミュニティツールキット](https://github.com/Microsoft/WindowsCommunityToolkit)からアプリケーションに統合します。

ソリューションエクスプローラーで**グラフのチュートリアル**プロジェクトを右クリックし、[ **Add > New Item...**.] を選択します。[**リソースファイル (. resw)**] を選択し`OAuth.resw` 、ファイルに名前を指定して、[**追加**] を選択します。 Visual Studio で新しいファイルが開いたら、次のように2つのリソースを作成します。

- **Name:**`AppId`, **Value:** アプリケーション登録ポータルで生成されたアプリ ID
- **Name:**`Scopes`、**値:**`User.Read Calendars.Read`

![Visual Studio エディターの OAuth w ファイルのスクリーンショット](./images/edit-resources-01.png)

> [!IMPORTANT]
> git などのソース管理を使用している場合は、この時点で、ソース管理`OAuth.resw`からファイルを除外して、アプリ ID が誤ってリークしないようにすることをお勧めします。

## <a name="configure-the-aadlogin-control"></a>AadLogin コントロールを構成する

最初に、リソースファイルから値を読み取るコードを追加します。 を`MainPage.xaml.cs`開き、次`using`のステートメントをファイルの先頭に追加します。

```cs
using Microsoft.Toolkit.Services.MicrosoftGraph;
```

行を次のコードに置き換えます。

```cs
// Load OAuth settings
var oauthSettings = Windows.ApplicationModel.Resources.ResourceLoader.GetForCurrentView("OAuth");
var appId = oauthSettings.GetString("AppId");
var scopes = oauthSettings.GetString("Scopes");

if (string.IsNullOrEmpty(appId) || string.IsNullOrEmpty(scopes))
{
    Notification.Show("Could not load OAuth Settings from resource file.");
}
else
{
    // Initialize Graph
    MicrosoftGraphService.Instance.AuthenticationModel = MicrosoftGraphEnums.AuthenticationModel.V2;
    MicrosoftGraphService.Instance.Initialize(appId,
        MicrosoftGraphEnums.ServicesToInitialize.UserProfile,
        scopes.Split(' '));

    // Navigate to HomePage.xaml
    RootFrame.Navigate(typeof(HomePage));
}
```

このコードでは、の`OAuth.resw`設定を読み込み、その値を`MicrosoftGraphService`使用してのグローバルインスタンスを初期化します。

次に、 `SignInCompleted` `AadLogin`コントロールにイベントのイベントハンドラーを追加します。 `MainPage.xaml`ファイルを開き、既存`<graphControls:AadLogin>`の要素を次のように置き換えます。

```xml
<graphControls:AadLogin x:Name="Login"
    HorizontalAlignment="Left"
    View="SmallProfilePhotoLeft"
    AllowSignInAsDifferentUser="False"
    SignInCompleted="Login_SignInCompleted"
    SignOutCompleted="Login_SignOutCompleted"
    />
```

その後、で`MainPage` `MainPage.xaml.cs`クラスに次の関数を追加します。

```cs
private void Login_SignInCompleted(object sender, Microsoft.Toolkit.Uwp.UI.Controls.Graph.SignInEventArgs e)
{
    // Set the auth state
    SetAuthState(true);
    // Reload the home page
    RootFrame.Navigate(typeof(HomePage));
}

private void Login_SignOutCompleted(object sender, EventArgs e)
{
    // Set the auth state
    SetAuthState(false);
    // Reload the home page
    RootFrame.Navigate(typeof(HomePage));
}
```

最後に、ソリューションエクスプローラーで、[**ホームページ**] を`HomePage.xaml.cs`展開し、を開きます。 行の`this.InitializeComponent();`後に次のコードを追加します。

```cs
if ((App.Current as App).IsAuthenticated)
{
    HomePageMessage.Text = "Welcome! Please use the menu to the left to select a view.";
}
```

アプリを再起動し、アプリの上部にある [**サインイン**] コントロールをクリックします。 サインインしたら、UI が変更され、サインインに成功したことを示します。

![サインインした後のアプリのスクリーンショット](./images/add-aad-auth-01.png)

> [!NOTE]
> この`AadLogin`コントロールは、アクセストークンの格納と更新のロジックを実装します。 トークンは、セキュリティで保護されたストレージに格納され、必要に応じて更新されます。