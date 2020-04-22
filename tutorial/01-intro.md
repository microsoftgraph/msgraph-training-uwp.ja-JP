<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="1aead-101">このチュートリアルでは、Microsoft Graph API を使用してユーザーの予定表情報を取得する、ユニバーサル Windows プラットフォーム (UWP) アプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1aead-101">This tutorial teaches you how to build a Universal Windows Platform (UWP) app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="1aead-102">完成したチュートリアルをダウンロードするだけで済む場合は、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-uwp)をダウンロードするか、クローンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="1aead-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-uwp).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1aead-103">前提条件</span><span class="sxs-lookup"><span data-stu-id="1aead-103">Prerequisites</span></span>

<span data-ttu-id="1aead-104">このチュートリアルを開始する前に、[開発モードがオンになっ](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)ている Windows 10 を実行しているコンピューターに[Visual Studio](https://visualstudio.microsoft.com/vs/)をインストールしておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="1aead-104">Before you start this tutorial, you should have [Visual Studio](https://visualstudio.microsoft.com/vs/) installed on a computer running Windows 10 with [Developer mode turned on](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development).</span></span> <span data-ttu-id="1aead-105">Visual Studio を持っていない場合は、「ダウンロードオプション」の前のリンクにアクセスしてください。</span><span class="sxs-lookup"><span data-stu-id="1aead-105">If you do not have Visual Studio, visit the previous link for download options.</span></span>

<span data-ttu-id="1aead-106">また、Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または Microsoft 職場または学校のアカウントを所有している必要があります。</span><span class="sxs-lookup"><span data-stu-id="1aead-106">You should also have either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span> <span data-ttu-id="1aead-107">Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="1aead-107">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="1aead-108">[新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。</span><span class="sxs-lookup"><span data-stu-id="1aead-108">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="1aead-109">[Office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="1aead-109">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="1aead-110">このチュートリアルは、Visual Studio 2019 version 16.5.0 を使用して作成されています。</span><span class="sxs-lookup"><span data-stu-id="1aead-110">This tutorial was written with Visual Studio 2019 version 16.5.0.</span></span> <span data-ttu-id="1aead-111">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。</span><span class="sxs-lookup"><span data-stu-id="1aead-111">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="watch-the-tutorial"></a><span data-ttu-id="1aead-112">チュートリアルを見る</span><span class="sxs-lookup"><span data-stu-id="1aead-112">Watch the tutorial</span></span>

<span data-ttu-id="1aead-113">このモジュールは、Office 開発 YouTube チャネルで記録されており、利用できます。</span><span class="sxs-lookup"><span data-stu-id="1aead-113">This module has been recorded and is available in the Office Development YouTube channel.</span></span>

<!-- markdownlint-disable MD033 MD034 -->
<br/>

> [!VIDEO https://www.youtube-nocookie.com/embed/oBYCBxkWMRA]
<!-- markdownlint-enable MD033 MD034 -->

## <a name="feedback"></a><span data-ttu-id="1aead-114">フィードバック</span><span class="sxs-lookup"><span data-stu-id="1aead-114">Feedback</span></span>

<span data-ttu-id="1aead-115">このチュートリアルに関するフィードバックは、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-uwp)に記入してください。</span><span class="sxs-lookup"><span data-stu-id="1aead-115">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-uwp).</span></span>
