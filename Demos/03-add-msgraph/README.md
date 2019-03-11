# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="137dd-101">完了したプロジェクトを実行する方法</span><span class="sxs-lookup"><span data-stu-id="137dd-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="137dd-102">前提条件</span><span class="sxs-lookup"><span data-stu-id="137dd-102">Prerequisites</span></span>

<span data-ttu-id="137dd-103">このフォルダーで完了したプロジェクトを実行するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="137dd-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="137dd-104">開発用コンピューターにインストールされている[Visual Studio](https://visualstudio.microsoft.com/vs/) 。</span><span class="sxs-lookup"><span data-stu-id="137dd-104">[Visual Studio](https://visualstudio.microsoft.com/vs/) installed on your development machine.</span></span> <span data-ttu-id="137dd-105">Visual Studio を持っていない場合は、「ダウンロードオプション」の前のリンクにアクセスしてください。</span><span class="sxs-lookup"><span data-stu-id="137dd-105">If you do not have Visual Studio, visit the previous link for download options.</span></span> <span data-ttu-id="137dd-106">(**注:** このチュートリアルは、Visual Studio 2017 バージョン15.81 で記述されています。</span><span class="sxs-lookup"><span data-stu-id="137dd-106">(**Note:** This tutorial was written with Visual Studio 2017 version 15.81.</span></span> <span data-ttu-id="137dd-107">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。)</span><span class="sxs-lookup"><span data-stu-id="137dd-107">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="137dd-108">Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または microsoft 職場または学校のアカウントのいずれか。</span><span class="sxs-lookup"><span data-stu-id="137dd-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="137dd-109">Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="137dd-109">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="137dd-110">[新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。</span><span class="sxs-lookup"><span data-stu-id="137dd-110">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="137dd-111">[office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="137dd-111">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-native-application-with-the-application-registration-portal"></a><span data-ttu-id="137dd-112">ネイティブアプリケーションをアプリケーション登録ポータルに登録する</span><span class="sxs-lookup"><span data-stu-id="137dd-112">Register a native application with the Application Registration Portal</span></span>

1. <span data-ttu-id="137dd-113">ブラウザーを開き、[アプリケーション登録ポータル](https://apps.dev.microsoft.com)に移動して、**個人アカウント**(別名: Microsoft アカウント) または**職場または学校のアカウント**を使用してログインします。</span><span class="sxs-lookup"><span data-stu-id="137dd-113">Open a browser and navigate to the [Application Registration Portal](https://apps.dev.microsoft.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="137dd-114">ページの上部にある [**アプリの追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="137dd-114">Select **Add an app** at the top of the page.</span></span>

    > <span data-ttu-id="137dd-115">**注:** ページに [**アプリの追加**] ボタンが複数表示されている場合は、[収束した**アプリ**] リストに対応するボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="137dd-115">**Note:** If you see more than one **Add an app** button on the page, select the one that corresponds to the **Converged apps** list.</span></span>

1. <span data-ttu-id="137dd-116">[**アプリケーションの登録**] ページで、[**アプリケーション名**] を「 **UWP Graph チュートリアル**」に設定し、[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="137dd-116">On the **Register your application** page, set the **Application Name** to **UWP Graph Tutorial** and select **Create**.</span></span>

    ![アプリ登録ポータル web サイトで新しいアプリを作成するスクリーンショット](../../../Images/arp-create-app-01.png)

1. <span data-ttu-id="137dd-118">[ **UWP Graph のチュートリアル登録**] ページの [**プロパティ**] セクションで、後で必要になるように**アプリケーション Id**をコピーします。</span><span class="sxs-lookup"><span data-stu-id="137dd-118">On the **UWP Graph Tutorial Registration** page, under the **Properties** section, copy the **Application Id** as you will need it later.</span></span>

    ![新しく作成されたアプリケーションの ID のスクリーンショット](../../../Images/arp-create-app-02.png)

1. <span data-ttu-id="137dd-120">[**プラットフォーム**] セクションまで下にスクロールします。</span><span class="sxs-lookup"><span data-stu-id="137dd-120">Scroll down to the **Platforms** section.</span></span>

    1. <span data-ttu-id="137dd-121">[**プラットフォームの追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="137dd-121">Select **Add Platform**.</span></span>
    1. <span data-ttu-id="137dd-122">[**プラットフォームの追加**] ダイアログで、[**ネイティブアプリケーション**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="137dd-122">In the **Add Platform** dialog, select **Native Application**.</span></span>

        ![アプリのプラットフォームを作成するスクリーンショット](../../../Images/arp-create-app-03.png)

1. <span data-ttu-id="137dd-124">ページの一番下までスクロールして、[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="137dd-124">Scroll to the bottom of the page and select **Save**.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="137dd-125">サンプルを構成する</span><span class="sxs-lookup"><span data-stu-id="137dd-125">Configure the sample</span></span>

1. <span data-ttu-id="137dd-126">ファイルの`OAuth.resw.example`名前を`OAuth.resw`に変更します。</span><span class="sxs-lookup"><span data-stu-id="137dd-126">Rename the `OAuth.resw.example` file to `OAuth.resw`.</span></span>
1. <span data-ttu-id="137dd-127">Visual `graph-tutorial.sln` Studio で開きます。</span><span class="sxs-lookup"><span data-stu-id="137dd-127">Open `graph-tutorial.sln` in Visual Studio.</span></span>
1. <span data-ttu-id="137dd-128">visual studio `OAuth.resw`でファイルを編集します。を`YOUR_APP_ID_HERE`アプリ登録ポータルで取得した**アプリケーション Id**に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="137dd-128">Edit the `OAuth.resw` file in visual studio.Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
1. <span data-ttu-id="137dd-129">ソリューションエクスプローラーで、**グラフチュートリアル**ソリューションを右クリックして、[ **NuGet パッケージの復元**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="137dd-129">In Solution Explorer, right-click the **graph-tutorial** solution and choose **Restore NuGet Packages**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="137dd-130">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="137dd-130">Run the sample</span></span>

<span data-ttu-id="137dd-131">Visual Studio で、 **F5**キーを押すか、デバッグ > を選択して**デバッグを開始**します。</span><span class="sxs-lookup"><span data-stu-id="137dd-131">In Visual Studio, press **F5** or choose **Debug > Start Debugging**.</span></span>