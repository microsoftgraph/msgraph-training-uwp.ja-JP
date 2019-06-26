<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="34ec9-101">このチュートリアルでは、Microsoft Graph API を使用してユーザーの予定表情報を取得する、ユニバーサル Windows プラットフォーム (UWP) アプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="34ec9-101">This tutorial teaches you how to build a Universal Windows Platform (UWP) app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="34ec9-102">完成したチュートリアルをダウンロードするだけで済む場合は、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-uwp)をダウンロードするか、クローンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="34ec9-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-uwp).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34ec9-103">前提条件</span><span class="sxs-lookup"><span data-stu-id="34ec9-103">Prerequisites</span></span>

<span data-ttu-id="34ec9-104">このチュートリアルを開始する前に、[開発モードがオンになっ](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)ている Windows 10 を実行しているコンピューターに[Visual Studio](https://visualstudio.microsoft.com/vs/)をインストールしておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="34ec9-104">Before you start this tutorial, you should have [Visual Studio](https://visualstudio.microsoft.com/vs/) installed on a computer running Windows 10 with [Developer mode turned on](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development).</span></span> <span data-ttu-id="34ec9-105">Visual Studio を持っていない場合は、「ダウンロードオプション」の前のリンクにアクセスしてください。</span><span class="sxs-lookup"><span data-stu-id="34ec9-105">If you do not have Visual Studio, visit the previous link for download options.</span></span>

> [!NOTE]
> <span data-ttu-id="34ec9-106">このチュートリアルは、Visual Studio 2017 version 15.8.1 を使用して作成されています。</span><span class="sxs-lookup"><span data-stu-id="34ec9-106">This tutorial was written with Visual Studio 2017 version 15.8.1.</span></span> <span data-ttu-id="34ec9-107">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。</span><span class="sxs-lookup"><span data-stu-id="34ec9-107">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="watch-the-tutorial"></a><span data-ttu-id="34ec9-108">チュートリアルを見る</span><span class="sxs-lookup"><span data-stu-id="34ec9-108">Watch the tutorial</span></span>

<span data-ttu-id="34ec9-109">このモジュールは、Office 開発 YouTube チャネルで記録されており、利用できます。</span><span class="sxs-lookup"><span data-stu-id="34ec9-109">This module has been recorded and is available in the Office Development YouTube channel.</span></span>

<!-- markdownlint-disable MD033 MD034 -->
<br/>

> [!VIDEO https://www.youtube-nocookie.com/embed/oBYCBxkWMRA]
<!-- markdownlint-enable MD033 MD034 -->

## <a name="feedback"></a><span data-ttu-id="34ec9-110">フィードバック</span><span class="sxs-lookup"><span data-stu-id="34ec9-110">Feedback</span></span>

<span data-ttu-id="34ec9-111">このチュートリアルに関するフィードバックは、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-uwp)に記入してください。</span><span class="sxs-lookup"><span data-stu-id="34ec9-111">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-uwp).</span></span>
