# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="33dcd-101">完了したプロジェクトを実行する方法</span><span class="sxs-lookup"><span data-stu-id="33dcd-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33dcd-102">前提条件</span><span class="sxs-lookup"><span data-stu-id="33dcd-102">Prerequisites</span></span>

<span data-ttu-id="33dcd-103">このフォルダーで完了したプロジェクトを実行するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="33dcd-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="33dcd-104">開発用コンピューターにインストールされている[Visual Studio](https://visualstudio.microsoft.com/vs/) 。</span><span class="sxs-lookup"><span data-stu-id="33dcd-104">[Visual Studio](https://visualstudio.microsoft.com/vs/) installed on your development machine.</span></span> <span data-ttu-id="33dcd-105">Visual Studio を持っていない場合は、「ダウンロードオプション」の前のリンクにアクセスしてください。</span><span class="sxs-lookup"><span data-stu-id="33dcd-105">If you do not have Visual Studio, visit the previous link for download options.</span></span> <span data-ttu-id="33dcd-106">(**注:** このチュートリアルは、Visual Studio 2017 バージョン15.81 で記述されています。</span><span class="sxs-lookup"><span data-stu-id="33dcd-106">(**Note:** This tutorial was written with Visual Studio 2017 version 15.81.</span></span> <span data-ttu-id="33dcd-107">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。)</span><span class="sxs-lookup"><span data-stu-id="33dcd-107">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="33dcd-108">Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または Microsoft 職場または学校のアカウントのいずれか。</span><span class="sxs-lookup"><span data-stu-id="33dcd-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="33dcd-109">Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="33dcd-109">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="33dcd-110">[新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。</span><span class="sxs-lookup"><span data-stu-id="33dcd-110">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="33dcd-111">[Office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="33dcd-111">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-native-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="33dcd-112">ネイティブアプリケーションを Azure Active Directory 管理センターに登録する</span><span class="sxs-lookup"><span data-stu-id="33dcd-112">Register a native application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="33dcd-113">ブラウザーを開き、[Azure Active Directory 管理センター](https://aad.portal.azure.com)へ移動して、**個人用アカウント** (別名: Microsoft アカウント)、または**職場/学校アカウント**を使用してログインします。</span><span class="sxs-lookup"><span data-stu-id="33dcd-113">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="33dcd-114">左側のナビゲーションで [ **Azure Active Directory** ] を選択し、[**管理**] の下にある [**アプリの登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="33dcd-114">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="33dcd-115">アプリの登録のスクリーンショット</span><span class="sxs-lookup"><span data-stu-id="33dcd-115">A screenshot of the App registrations</span></span> ](/tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="33dcd-116">**[新規登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="33dcd-116">Select **New registration**.</span></span> <span data-ttu-id="33dcd-117">**[アプリケーションを登録]** ページで、次のように値を設定します。</span><span class="sxs-lookup"><span data-stu-id="33dcd-117">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="33dcd-118">`UWP Graph Tutorial` に **[名前]** を設定します。</span><span class="sxs-lookup"><span data-stu-id="33dcd-118">Set **Name** to `UWP Graph Tutorial`.</span></span>
    - <span data-ttu-id="33dcd-119">[**サポートされているアカウントの種類**] を [**任意の組織のディレクトリ内のアカウントと個人用の Microsoft アカウント**] に設定します。</span><span class="sxs-lookup"><span data-stu-id="33dcd-119">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="33dcd-120">[**リダイレクト URI**] で、ドロップダウンを [**パブリッククライアント (モバイル & デスクトップ)**] に変更し`urn:ietf:wg:oauth:2.0:oob`、値をに設定します。</span><span class="sxs-lookup"><span data-stu-id="33dcd-120">Under **Redirect URI**, change the dropdown to **Public client (mobile & desktop)**, and set the value to `urn:ietf:wg:oauth:2.0:oob`.</span></span>

    ![[アプリケーションの登録] ページのスクリーンショット](/tutorial/images/aad-register-app.png)

1. <span data-ttu-id="33dcd-122">[**登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="33dcd-122">Choose **Register**.</span></span> <span data-ttu-id="33dcd-123">**UWP グラフのチュートリアル**ページで、**アプリケーション (クライアント) ID**の値をコピーして保存します。次の手順で必要になります。</span><span class="sxs-lookup"><span data-stu-id="33dcd-123">On the **UWP Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新しいアプリの登録のアプリケーション ID のスクリーンショット](/tutorial/images/aad-application-id.png)

## <a name="configure-the-sample"></a><span data-ttu-id="33dcd-125">サンプルを構成する</span><span class="sxs-lookup"><span data-stu-id="33dcd-125">Configure the sample</span></span>

1. <span data-ttu-id="33dcd-126">ファイルの`OAuth.resw.example`名前を`OAuth.resw`に変更します。</span><span class="sxs-lookup"><span data-stu-id="33dcd-126">Rename the `OAuth.resw.example` file to `OAuth.resw`.</span></span>
1. <span data-ttu-id="33dcd-127">Visual `graph-tutorial.sln` Studio で開きます。</span><span class="sxs-lookup"><span data-stu-id="33dcd-127">Open `graph-tutorial.sln` in Visual Studio.</span></span>
1. <span data-ttu-id="33dcd-128">Visual studio `OAuth.resw`でファイルを編集します。を`YOUR_APP_ID_HERE`アプリ登録ポータルで取得した**アプリケーション Id**に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="33dcd-128">Edit the `OAuth.resw` file in visual studio.Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
1. <span data-ttu-id="33dcd-129">ソリューションエクスプローラーで、**グラフチュートリアル**ソリューションを右クリックして、[ **NuGet パッケージの復元**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="33dcd-129">In Solution Explorer, right-click the **graph-tutorial** solution and choose **Restore NuGet Packages**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="33dcd-130">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="33dcd-130">Run the sample</span></span>

<span data-ttu-id="33dcd-131">Visual Studio で、 **F5**キーを押すか、デバッグ > 選択して**デバッグを開始**します。</span><span class="sxs-lookup"><span data-stu-id="33dcd-131">In Visual Studio, press **F5** or choose **Debug > Start Debugging**.</span></span>