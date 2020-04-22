<!-- markdownlint-disable MD002 MD041 -->

この演習では、Azure AD での認証をサポートするために、前の手順で作成したアプリケーションを拡張します。 これは、Microsoft Graph を呼び出すために必要な OAuth アクセストークンを取得するために必要です。 この手順では、 [Windows Graph コントロール](https://github.com/windows-toolkit/Graph-Controls)から**loginbutton**コントロールをアプリケーションに統合します。

1. ソリューションエクスプローラーで**Graphtutorial**プロジェクトを右クリックし、[ **Add > New Item...**.] を選択します。[**リソースファイル (. resw)**] を選択し`OAuth.resw` 、ファイルに名前を指定して、[**追加**] を選択します。 Visual Studio で新しいファイルが開いたら、次のように2つのリソースを作成します。

    - **名前:** `AppId`、**値:** アプリケーション登録ポータルで生成されたアプリ ID
    - **名前:** `Scopes`、**値:**`User.Read Calendars.Read`

    ![Visual Studio エディターの OAuth w ファイルのスクリーンショット](./images/edit-resources-01.png)

    > [!IMPORTANT]
    > Git などのソース管理を使用している場合は、この時点で、ソース管理`OAuth.resw`からファイルを除外して、アプリ ID が誤ってリークしないようにすることをお勧めします。

## <a name="configure-the-loginbutton-control"></a>LoginButton コントロールを構成する

1. を`MainPage.xaml.cs`開き、次`using`のステートメントをファイルの先頭に追加します。

    ```csharp
    using Microsoft.Toolkit.Graph.Providers;
    ```

1. 既存のコンストラクターを次のように置き換えます。

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ConstructorSnippet":::

    このコードでは、の`OAuth.resw`設定を読み込み、その値を使用して msal プロバイダーを初期化します。

1. `ProviderUpdated`イベントのイベントハンドラーをに追加し`ProviderManager`ます。 次の関数を `MainPage` クラスに追加します。

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ProviderUpdatedSnippet":::

    このイベントは、プロバイダーが変更されたとき、またはプロバイダーの状態が変更されたときにトリガーされます。

1. ソリューションエクスプローラーで、[**ホームページ] .xaml**を`HomePage.xaml.cs`展開し、を開きます。 既存のコンストラクターを次のように置き換えます。

    :::code language="csharp" source="../demo/GraphTutorial/HomePage.xaml.cs" id="ConstructorSnippet":::

1. アプリを再起動し、アプリの上部にある [**サインイン**] コントロールをクリックします。 サインインしたら、UI が変更され、サインインに成功したことを示します。

    ![サインインした後のアプリのスクリーンショット](./images/add-aad-auth-01.png)

    > [!NOTE]
    > この`ButtonLogin`コントロールは、アクセストークンの格納と更新のロジックを実装します。 トークンは、セキュリティで保護されたストレージに格納され、必要に応じて更新されます。
