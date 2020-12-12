<!-- markdownlint-disable MD002 MD041 -->

この演習では、前の演習のアプリケーションを拡張して、Azure AD での認証をサポートします。 これは、Microsoft Graph を呼び出すのに必要な OAuth アクセス トークンを取得するために必要です。 この手順では [、Windows Graph](https://github.com/windows-toolkit/Graph-Controls)コントロールの **LoginButton** コントロールをアプリケーションに統合します。

1. ソリューション エクスプローラーで **GraphTu solutionl** プロジェクトを右クリックし、[新しいアイテムの> **を選択します**。Choose **Resources File (.resw)**, name the file `OAuth.resw` and select **Add**. 新しいファイルが開いたら、次Visual Studio 2 つのリソースを作成します。

    - **名前:** `AppId` 、 **値:** アプリケーション登録ポータルで生成したアプリ ID
    - **名前:** `Scopes` 、**値:**`User.Read User.ReadBasic.All People.Read MailboxSettings.Read Calendars.ReadWrite`

    ![新しいエディターの OAuth.resw ファイルVisual Studioスクリーンショット](./images/edit-resources-01.png)

    > [!IMPORTANT]
    > git などのソース管理を使っている場合は、アプリ ID が誤って漏洩しないように、ファイルをソース管理から除外する良い時期 `OAuth.resw` です。

## <a name="configure-the-loginbutton-control"></a>LoginButton コントロールを構成する

1. 次 `MainPage.xaml.cs` のステートメントを `using` 開き、ファイルの一番上に追加します。

    ```csharp
    using Microsoft.Toolkit.Graph.Providers;
    ```

1. 既存のコンストラクターを次のコンストラクターに置き換える。

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ConstructorSnippet":::

    このコードは、これらの値から設定を読 `OAuth.resw` み込み、MSAL プロバイダーを初期化します。

1. 次に、イベントのイベント ハンドラー `ProviderUpdated` を追加します `ProviderManager` 。 次の関数を `MainPage` クラスに追加します。

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ProviderUpdatedSnippet":::

    このイベントは、プロバイダーが変更された場合、またはプロバイダーの状態が変更されると発生します。

1. ソリューション エクスプローラーで **、HomePage.xaml を展開** して開きます `HomePage.xaml.cs` 。 既存のコンストラクターを次のコンストラクターに置き換える。

    :::code language="csharp" source="../demo/GraphTutorial/HomePage.xaml.cs" id="ConstructorSnippet":::

1. アプリを再起動し、アプリ **の上部** にある [サインイン] コントロールをクリックします。 サインインが完了すると、UI が変更して、正常にサインインされたことを示す必要があります。

    ![サインイン後のアプリのスクリーンショット](./images/add-aad-auth-01.png)

    > [!NOTE]
    > コントロール `ButtonLogin` は、アクセス トークンを保存および更新するロジックを実装します。 トークンはセキュリティで保護されたストレージに格納され、必要に応じて更新されます。
