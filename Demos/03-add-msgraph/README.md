# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="a18ad-101">完了したプロジェクトを実行する方法</span><span class="sxs-lookup"><span data-stu-id="a18ad-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a18ad-102">前提条件</span><span class="sxs-lookup"><span data-stu-id="a18ad-102">Prerequisites</span></span>

<span data-ttu-id="a18ad-103">このフォルダーで完了したプロジェクトを実行するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="a18ad-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="a18ad-104">開発用コンピューターにインストールされている[Visual Studio](https://visualstudio.microsoft.com/vs/) 。</span><span class="sxs-lookup"><span data-stu-id="a18ad-104">[Visual Studio](https://visualstudio.microsoft.com/vs/) installed on your development machine.</span></span> <span data-ttu-id="a18ad-105">Visual Studio を持っていない場合は、「ダウンロードオプション」の前のリンクにアクセスしてください。</span><span class="sxs-lookup"><span data-stu-id="a18ad-105">If you do not have Visual Studio, visit the previous link for download options.</span></span> <span data-ttu-id="a18ad-106">(**注:** このチュートリアルは、Visual Studio 2017 バージョン15.81 で記述されています。</span><span class="sxs-lookup"><span data-stu-id="a18ad-106">(**Note:** This tutorial was written with Visual Studio 2017 version 15.81.</span></span> <span data-ttu-id="a18ad-107">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。)</span><span class="sxs-lookup"><span data-stu-id="a18ad-107">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="a18ad-108">Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または Microsoft 職場または学校のアカウントのいずれか。</span><span class="sxs-lookup"><span data-stu-id="a18ad-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="a18ad-109">Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="a18ad-109">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="a18ad-110">[新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。</span><span class="sxs-lookup"><span data-stu-id="a18ad-110">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="a18ad-111">[Office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="a18ad-111">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-native-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="a18ad-112">ネイティブアプリケーションを Azure Active Directory 管理センターに登録する</span><span class="sxs-lookup"><span data-stu-id="a18ad-112">Register a native application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="a18ad-113">ブラウザーを開き、[Azure Active Directory 管理センター](https://aad.portal.azure.com)へ移動して、**個人用アカウント** (別名: Microsoft アカウント)、または**職場/学校アカウント**を使用してログインします。</span><span class="sxs-lookup"><span data-stu-id="a18ad-113">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="a18ad-114">左側のナビゲーションで [ **Azure Active Directory** ] を選択し、[**管理**] の下にある [**アプリの登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a18ad-114">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="a18ad-115">アプリの登録のスクリーンショット</span><span class="sxs-lookup"><span data-stu-id="a18ad-115">A screenshot of the App registrations</span></span> ](/tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="a18ad-116">**[新規登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a18ad-116">Select **New registration**.</span></span> <span data-ttu-id="a18ad-117">**[アプリケーションを登録]** ページで、次のように値を設定します。</span><span class="sxs-lookup"><span data-stu-id="a18ad-117">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="a18ad-118">`UWP Graph Tutorial` に **[名前]** を設定します。</span><span class="sxs-lookup"><span data-stu-id="a18ad-118">Set **Name** to `UWP Graph Tutorial`.</span></span>
    - <span data-ttu-id="a18ad-119">**[サポートされているアカウントの種類]** を **[任意の組織のディレクトリ内のアカウントと個人用の Microsoft アカウント]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="a18ad-119">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="a18ad-120">**[リダイレクト URI]** を空のままにします。</span><span class="sxs-lookup"><span data-stu-id="a18ad-120">Leave **Redirect URI** empty.</span></span>

    ![[アプリケーションの登録] ページのスクリーンショット](/tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="a18ad-122">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a18ad-122">Choose **Register**.</span></span> <span data-ttu-id="a18ad-123">**UWP グラフのチュートリアル**ページで、**アプリケーション (クライアント) ID**の値をコピーして保存します。次の手順で必要になります。</span><span class="sxs-lookup"><span data-stu-id="a18ad-123">On the **UWP Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新しいアプリの登録のアプリケーション ID のスクリーンショット](/tutorial/images/aad-application-id.png)

1. <span data-ttu-id="a18ad-125">[**リダイレクト URI を追加する**] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="a18ad-125">Select the **Add a Redirect URI** link.</span></span> <span data-ttu-id="a18ad-126">[**リダイレクト uri** ] ページで、[**パブリッククライアント (モバイル、デスクトップ)] セクションの推奨されるリダイレクト uri**を見つけます。</span><span class="sxs-lookup"><span data-stu-id="a18ad-126">On the **Redirect URIs** page, locate the **Suggested Redirect URIs for public clients (mobile, desktop)** section.</span></span> <span data-ttu-id="a18ad-127">`urn:ietf:wg:oauth:2.0:oob` URI を選択し、[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a18ad-127">Select the `urn:ietf:wg:oauth:2.0:oob` URI, then choose **Save**.</span></span>

    ![リダイレクト Uri ページのスクリーンショット](/tutorial/images/aad-redirect-uris.png)

## <a name="configure-the-sample"></a><span data-ttu-id="a18ad-129">サンプルを構成する</span><span class="sxs-lookup"><span data-stu-id="a18ad-129">Configure the sample</span></span>

1. <span data-ttu-id="a18ad-130">ファイルの`OAuth.resw.example`名前を`OAuth.resw`に変更します。</span><span class="sxs-lookup"><span data-stu-id="a18ad-130">Rename the `OAuth.resw.example` file to `OAuth.resw`.</span></span>
1. <span data-ttu-id="a18ad-131">Visual `graph-tutorial.sln` Studio で開きます。</span><span class="sxs-lookup"><span data-stu-id="a18ad-131">Open `graph-tutorial.sln` in Visual Studio.</span></span>
1. <span data-ttu-id="a18ad-132">Visual studio `OAuth.resw`でファイルを編集します。を`YOUR_APP_ID_HERE`アプリ登録ポータルで取得した**アプリケーション Id**に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a18ad-132">Edit the `OAuth.resw` file in visual studio.Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
1. <span data-ttu-id="a18ad-133">ソリューションエクスプローラーで、**グラフチュートリアル**ソリューションを右クリックして、[ **NuGet パッケージの復元**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a18ad-133">In Solution Explorer, right-click the **graph-tutorial** solution and choose **Restore NuGet Packages**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="a18ad-134">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="a18ad-134">Run the sample</span></span>

<span data-ttu-id="a18ad-135">Visual Studio で、 **F5**キーを押すか、デバッグ > を選択して**デバッグを開始**します。</span><span class="sxs-lookup"><span data-stu-id="a18ad-135">In Visual Studio, press **F5** or choose **Debug > Start Debugging**.</span></span>