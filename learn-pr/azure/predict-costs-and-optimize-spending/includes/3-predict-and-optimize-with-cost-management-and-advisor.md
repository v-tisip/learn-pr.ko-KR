<span data-ttu-id="0a64d-101">Azure에 서비스를 배포하기 전에 비용을 예상하는 방법에 대해 배웠지만 리소스가 이미 배포되어 있는 경우에는 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="0a64d-101">We learned how to estimate your costs before you deploy services on Azure, but what if you already have resources deployed?</span></span> <span data-ttu-id="0a64d-102">이미 발생한 비용은 어떻게 파악하나요?</span><span class="sxs-lookup"><span data-stu-id="0a64d-102">How do you get visibility into the costs you're already accruing?</span></span> <span data-ttu-id="0a64d-103">이전에 솔루션을 Azure에 배포했으나 가상 머신의 크기를 적절하게 지정했는지 확인하고 청구 금액이 얼마일지 예상해 볼 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="0a64d-103">If we had deployed our previous solution to Azure and now want to make sure that we've sized the virtual machines properly and predict how much our bill will be, how can we do this?</span></span> <span data-ttu-id="0a64d-104">이 문제를 해결하는 데 사용할 수 있는 Azure의 몇 가지 도구를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-104">Let's look at a few tools on Azure that you can use to help you solve this problem.</span></span>

## <a name="what-is-azure-advisor"></a><span data-ttu-id="0a64d-105">Azure Advisor란?</span><span class="sxs-lookup"><span data-stu-id="0a64d-105">What is Azure Advisor?</span></span> 

<span data-ttu-id="0a64d-106">**Azure Advisor**는 Azure에 빌드된 무료 서비스로, 고가용성과 보안, 성능, 비용에 대한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-106">**Azure Advisor** is a free service built into Azure that provides recommendations on high availability, security, performance, and cost.</span></span> <span data-ttu-id="0a64d-107">Advisor는 배포된 서비스를 분석하여 이러한 네 영역에서 환경을 개선할 방법을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-107">Advisor analyzes your deployed services and looks for ways to improve your environment across those four areas.</span></span> <span data-ttu-id="0a64d-108">여기서는 비용 권장 사항을 중점적으로 살펴보지만, 시간을 내서 다른 권장 사항도 검토해 보세요.</span><span class="sxs-lookup"><span data-stu-id="0a64d-108">We'll focus on the cost recommendations, but you'll want to take some time to review the other recommendations as well.</span></span>

<span data-ttu-id="0a64d-109">Advisor에서 비용 권장 사항을 제공하는 영역은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-109">Advisor makes cost recommendations in the following areas:</span></span> 

1. <span data-ttu-id="0a64d-110">**프로비전되지 않은 Azure ExpressRoute 회로를 제거하여 비용을 절감합니다.**</span><span class="sxs-lookup"><span data-stu-id="0a64d-110">**Reduce costs by eliminating unprovisioned Azure ExpressRoute circuits.**</span></span> 
    <span data-ttu-id="0a64d-111">이 서비스는 공급자 상태가 1개월 넘게 ‘프로비전되지 않음’인 ExpressRoute 회로를 식별하고, 연결 공급자로 회로를 프로비전하지 않으려는 경우 회로를 삭제할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-111">This identifies ExpressRoute circuits that have been in the provider status of *Not Provisioned* for more than one month and recommends deleting the circuit if you aren't planning to provision the circuit with your connectivity provider.</span></span>

2. <span data-ttu-id="0a64d-112">**예약 인스턴스를 구입하여 종량제보다 비용을 절감합니다.**</span><span class="sxs-lookup"><span data-stu-id="0a64d-112">**Buy reserved instances to save money over pay-as-you-go.**</span></span> 
    <span data-ttu-id="0a64d-113">이 서비스는 지난 30일 동안의 가상 머신 사용량을 검토하여 예약 인스턴스를 구매하면 앞으로 비용을 절감할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-113">This will review your virtual machine usage over the last 30 days and determine if you could save money in the future by purchasing reserved instances.</span></span> <span data-ttu-id="0a64d-114">Advisor는 잠재적으로 절감액이 가장 큰 지역과 크기를 보여주고, 예약 인스턴스 구매로 얻을 수 있는 예상 절감액을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-114">Advisor will show you the regions and sizes where you potentially have the most savings and will show you the estimated savings you might achieve from purchasing reserved instances.</span></span>
    
3. <span data-ttu-id="0a64d-115">**사용률이 낮은 가상 머신을 적합한 크기로 지정하거나 종료합니다.**</span><span class="sxs-lookup"><span data-stu-id="0a64d-115">**Right-size or shutdown underutilized virtual machines.**</span></span> 
    <span data-ttu-id="0a64d-116">이 서비스는 14일 동안 가상 머신 사용량을 모니터링하여 사용률이 낮은 가상 머신을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-116">This monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="0a64d-117">4일 이상 평균 CPU 사용률이 5% 이하이고 네트워크 사용량이 7MB 이하인 가상 머신은 사용률이 낮은 가상 머신으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-117">Virtual machines whose average CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span> <span data-ttu-id="0a64d-118">평균 CPU 활용률 임계값은 최대 20%까지 조정 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-118">The average CPU utilization threshold is adjustable up to 20 percent.</span></span> <span data-ttu-id="0a64d-119">이렇게 사용률이 낮은 가상 머신을 식별하면 더 작은 인스턴스 유형으로 크기를 조정하도록 결정하여 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-119">By identifying these underutilized virtual machines, you can decide to resize them to a smaller instance type, reducing your costs.</span></span>

<span data-ttu-id="0a64d-120">포털에서 Azure Advisor를 찾을 수 있는 위치를 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-120">Let's take a look at where you can find Azure Advisor in the portal.</span></span> <span data-ttu-id="0a64d-121">먼저, [https://portal.azure.com](https://portal.azure.com)에서 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-121">First, sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span> <span data-ttu-id="0a64d-122">**모든 서비스**를 클릭하면 **관리 도구** 범주에 **Advisor**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-122">Click on **All Services**, and in the **Management Tools** category, you will see **Advisor**.</span></span> <span data-ttu-id="0a64d-123">필터 상자에 **Advisor**를 입력하여 해당 서비스를 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-123">You can also type **Advisor** in the filter box to filter on just that service.</span></span> 

<span data-ttu-id="0a64d-124">Advisor를 클릭하면 해당 구독에 대한 모든 권장 사항을 볼 수 있는 Advisor 권장 사항 대시보드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-124">Click on Advisor, and you'll be taken to the Advisor recommendations dashboard where you can see all recommendations for your subscription.</span></span> <span data-ttu-id="0a64d-125">권장 사항 범주마다 하나의 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-125">You'll see a box for each category of recommendations.</span></span> 

> [!NOTE]
> <span data-ttu-id="0a64d-126">Advisor에 비용에 대한 권장 사항이 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-126">You might not have any recommendations on cost in Advisor.</span></span> <span data-ttu-id="0a64d-127">평가가 아직 완료되지 않았기 때문일 수도 있고 Advisor의 권장 사항이 없기 때문일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-127">This could be because assessments have not yet completed or simply because Advisor has no recommendations.</span></span>

![Advisor 권장 사항](../images/advisor-recommendations.png)

<span data-ttu-id="0a64d-129">**비용** 상자를 클릭하면 Advisor의 권장 사항을 볼 수 있는 자세한 권장 사항으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-129">Clicking on the **Cost** box will take you to detailed recommendations for where you can see the recommendations that Advisor has.</span></span>

![Advisor 비용 권장 사항](../images/advisor-cost-recommendations.png)

<span data-ttu-id="0a64d-131">권장 사항 하나를 클릭하면 해당 권장 사항에 대한 세부 정보로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-131">Clicking on any recommendation will take you to the details for that specific recommendation.</span></span> <span data-ttu-id="0a64d-132">그러면 지출을 줄이도록 가상 머신 크기를 조정하는 것과 같은 특정 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-132">Then you'll be able to take specific action, such as resizing virtual machines to reduce spending.</span></span>

![Advisor VM 크기 조정 권장 사항](../images/advisor-resize-vm.png)

<span data-ttu-id="0a64d-134">이러한 권장 사항은 모두 비효율적으로 비용을 지출하고 있는 부분에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-134">These recommendations are all places where you might be inefficiently spending money.</span></span> <span data-ttu-id="0a64d-135">비용을 절감할 부분을 찾고 있는 경우 이러한 권장 사항을 확인하여 특정 조치를 시작하고 지속적으로 다시 방문하여 확인하면 많은 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-135">They're a great place to start and continue to revisit when looking for places to reduce costs.</span></span> <span data-ttu-id="0a64d-136">이 예에서는 권장 사항을 적용하는 경우 매월 약 $700를 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-136">In our example, there's an opportunity for us to save around $700 per month if we take these recommendations.</span></span> <span data-ttu-id="0a64d-137">이러한 절감액은 증가될 수 있으므로 네 영역 모두에서 권장 사항을 정기적으로 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-137">This savings adds up, so be sure to review this periodically for recommendations across all four areas.</span></span>

## <a name="azure-cost-management"></a><span data-ttu-id="0a64d-138">Azure Cost Management</span><span class="sxs-lookup"><span data-stu-id="0a64d-138">Azure Cost Management</span></span>

<span data-ttu-id="0a64d-139">Azure Cost Management는 클라우드 비용이 발생하는 부분을 보다 확실하게 파악하기 위해 사용할 수 있는, 또 하나의 무료 기본 제공 Azure 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-139">Azure Cost Management is another free, built-in Azure tool that can be used to gain greater insights into where your cloud money is going.</span></span> <span data-ttu-id="0a64d-140">비용을 지출하는 서비스와 설정된 예산 대비 지출을 추적하는 방법에 대한 기록 분석 결과를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-140">You can see historical breakdowns of what services you are spending your money on and how it is tracking against budgets that you have set.</span></span> <span data-ttu-id="0a64d-141">예산을 설정하고, 보고서를 예약하고, 비용 영역을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-141">You can set budgets, schedule reports, and analyze your cost areas.</span></span>

![Cost Management](../images/cost-management.png)

## <a name="cloudyn"></a><span data-ttu-id="0a64d-143">Cloudyn</span><span class="sxs-lookup"><span data-stu-id="0a64d-143">Cloudyn</span></span> 

<span data-ttu-id="0a64d-144">Microsoft 자회사인 Cloudyn을 통해 Azure 리소스와 Amazon Web Services 및 Google을 포함한 다른 클라우드 공급자에 대한 클라우드 사용량 및 지출을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-144">Cloudyn, a Microsoft subsidiary, allows you to track cloud usage and expenditures for your Azure resources and other cloud providers including Amazon Web Services and Google.</span></span> <span data-ttu-id="0a64d-145">이해하기 쉬운 대시보드 보고서는 비용 할당과 쇼백 또는 차지백에도 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-145">Easy-to-understand dashboard reports help with cost allocation and showbacks or chargebacks as well.</span></span> <span data-ttu-id="0a64d-146">Cost Management를 통해 관리하고 조정할 수 있는 사용률이 낮은 리소스를 식별하여 클라우드 소비를 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-146">Cost Management helps optimize your cloud spending by identifying underutilized resources that you can then manage and adjust.</span></span> <span data-ttu-id="0a64d-147">Azure에 대한 사용은 무료이며, 프리미엄 지원을 받거나 다른 클라우드의 데이터를 볼 수 있는 유료 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-147">Usage for Azure is free, and there are paid options for premium support and to view data from other clouds.</span></span> 

![Cloudyn 관리 대시보드](../images/cloudyn-mgt-dash.png)

## <a name="summary"></a><span data-ttu-id="0a64d-149">요약</span><span class="sxs-lookup"><span data-stu-id="0a64d-149">Summary</span></span>

<span data-ttu-id="0a64d-150">살펴본 것처럼 Azure에서는 클라우드 지출을 추적 및 예측하는 데 사용하고 현재 환경을 비용 관점에서 볼 때 비효율적인 부분을 파악하는 데 사용할 수 있는 여러 도구를 추가 비용 없이 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-150">As you can see, there are several tools available for no cost on Azure that you can use to track and predict your cloud spend and identify where your environment may be inefficient from a cost perspective.</span></span> <span data-ttu-id="0a64d-151">이러한 도구에서 제공하는 보고서와 권장 사항을 정기적으로 검토하여 전체 클라우드 공간에서 비용을 절감할 수 있도록 하세요.</span><span class="sxs-lookup"><span data-stu-id="0a64d-151">You'll want to make sure you make it a regular practice to review the reports and recommendations that these tools make available, so you can unlock savings across your cloud footprint.</span></span> <span data-ttu-id="0a64d-152">이제 인프라 비용을 절감하는 데 도움이 될 몇 가지 모범 사례를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a64d-152">Now let's take a look at some best practices to reduce your infrastructure costs.</span></span>