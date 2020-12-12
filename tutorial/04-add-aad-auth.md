<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="b7e8d-101">この演習では、前の演習のアプリケーションを拡張して、Azure AD での認証をサポートします。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="b7e8d-102">これは、Microsoft Graph を呼び出すのに必要な OAuth アクセス トークンを取得するために必要です。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="b7e8d-103">この手順では [、Windows Graph](https://github.com/windows-toolkit/Graph-Controls)コントロールの **LoginButton** コントロールをアプリケーションに統合します。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-103">In this step you will integrate the **LoginButton** control from the [Windows Graph Controls](https://github.com/windows-toolkit/Graph-Controls) into the application.</span></span>

1. <span data-ttu-id="b7e8d-104">ソリューション エクスプローラーで **GraphTu solutionl** プロジェクトを右クリックし、[新しいアイテムの> **を選択します**。Choose **Resources File (.resw)**, name the file `OAuth.resw` and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="b7e8d-104">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Resources File (.resw)**, name the file `OAuth.resw` and select **Add**.</span></span> <span data-ttu-id="b7e8d-105">新しいファイルが開いたら、次Visual Studio 2 つのリソースを作成します。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-105">When the new file opens in Visual Studio, create two resources as follows.</span></span>

    - <span data-ttu-id="b7e8d-106">**名前:** `AppId` 、 **値:** アプリケーション登録ポータルで生成したアプリ ID</span><span class="sxs-lookup"><span data-stu-id="b7e8d-106">**Name:** `AppId`, **Value:** the app ID you generated in Application Registration Portal</span></span>
    - <span data-ttu-id="b7e8d-107">**名前:** `Scopes` 、**値:**`User.Read User.ReadBasic.All People.Read MailboxSettings.Read Calendars.ReadWrite`</span><span class="sxs-lookup"><span data-stu-id="b7e8d-107">**Name:** `Scopes`, **Value:** `User.Read User.ReadBasic.All People.Read MailboxSettings.Read Calendars.ReadWrite`</span></span>

    ![新しいエディターの OAuth.resw ファイルVisual Studioスクリーンショット](./images/edit-resources-01.png)

    > [!IMPORTANT]
    > <span data-ttu-id="b7e8d-109">git などのソース管理を使っている場合は、アプリ ID が誤って漏洩しないように、ファイルをソース管理から除外する良い時期 `OAuth.resw` です。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-109">If you're using source control such as git, now would be a good time to exclude the `OAuth.resw` file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="configure-the-loginbutton-control"></a><span data-ttu-id="b7e8d-110">LoginButton コントロールを構成する</span><span class="sxs-lookup"><span data-stu-id="b7e8d-110">Configure the LoginButton control</span></span>

1. <span data-ttu-id="b7e8d-111">次 `MainPage.xaml.cs` のステートメントを `using` 開き、ファイルの一番上に追加します。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-111">Open `MainPage.xaml.cs` and add the following `using` statement to the top of the file.</span></span>

    ```csharp
    using Microsoft.Toolkit.Graph.Providers;
    ```

1. <span data-ttu-id="b7e8d-112">既存のコンストラクターを次のコンストラクターに置き換える。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-112">Replace the existing constructor with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ConstructorSnippet":::

    <span data-ttu-id="b7e8d-113">このコードは、これらの値から設定を読 `OAuth.resw` み込み、MSAL プロバイダーを初期化します。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-113">This code loads the settings from `OAuth.resw` and initializes the MSAL provider with those values.</span></span>

1. <span data-ttu-id="b7e8d-114">次に、イベントのイベント ハンドラー `ProviderUpdated` を追加します `ProviderManager` 。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-114">Now add an event handler for the `ProviderUpdated` event on the `ProviderManager`.</span></span> <span data-ttu-id="b7e8d-115">次の関数を `MainPage` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-115">Add the following function to the `MainPage` class.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ProviderUpdatedSnippet":::

    <span data-ttu-id="b7e8d-116">このイベントは、プロバイダーが変更された場合、またはプロバイダーの状態が変更されると発生します。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-116">This event triggers when the provider changes, or when the provider state changes.</span></span>

1. <span data-ttu-id="b7e8d-117">ソリューション エクスプローラーで **、HomePage.xaml を展開** して開きます `HomePage.xaml.cs` 。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-117">In Solution Explorer, expand **HomePage.xaml** and open `HomePage.xaml.cs`.</span></span> <span data-ttu-id="b7e8d-118">既存のコンストラクターを次のコンストラクターに置き換える。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-118">Replace the existing constructor with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/HomePage.xaml.cs" id="ConstructorSnippet":::

1. <span data-ttu-id="b7e8d-119">アプリを再起動し、アプリ **の上部** にある [サインイン] コントロールをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-119">Restart the app and click the **Sign In** control at the top of the app.</span></span> <span data-ttu-id="b7e8d-120">サインインが完了すると、UI が変更して、正常にサインインされたことを示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-120">Once you've signed in, the UI should change to indicate that you've successfully signed-in.</span></span>

    ![サインイン後のアプリのスクリーンショット](./images/add-aad-auth-01.png)

    > [!NOTE]
    > <span data-ttu-id="b7e8d-122">コントロール `ButtonLogin` は、アクセス トークンを保存および更新するロジックを実装します。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-122">The `ButtonLogin` control implements the logic of storing and refreshing the access token for you.</span></span> <span data-ttu-id="b7e8d-123">トークンはセキュリティで保護されたストレージに格納され、必要に応じて更新されます。</span><span class="sxs-lookup"><span data-stu-id="b7e8d-123">The tokens are stored in secure storage and refreshed as needed.</span></span>
