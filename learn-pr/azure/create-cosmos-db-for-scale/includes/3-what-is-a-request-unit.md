<span data-ttu-id="50be5-101">다음으로 데이터베이스에 대한 데이터 처리량을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-101">Next we'll consider the data throughout for our database.</span></span> <span data-ttu-id="50be5-102">비즈니스 요구 사항에 대한 트랜잭션 볼륨을 처리할 수 있는지 확인하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-102">This is important to ensure we can handle the volume of transactions for our business needs.</span></span> <span data-ttu-id="50be5-103">처리량 요구 사항이 항상 일관된 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-103">Throughput requirements aren't always consistent.</span></span> <span data-ttu-id="50be5-104">예를 들어 판매 또는 휴일 중에 크기를 조정해야 하는 쇼핑 웹 사이트를 빌드하고 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-104">For example, you may be building a shopping website that needs to scale during sales or holidays.</span></span> <span data-ttu-id="50be5-105">먼저 데이터베이스 처리량 요구 사항을 예측해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-105">We'll start estimating your database throughput requirements.</span></span>

## <a name="what-is-database-throughput"></a><span data-ttu-id="50be5-106">데이터베이스 처리량이란?</span><span class="sxs-lookup"><span data-stu-id="50be5-106">What is database throughput?</span></span> 

<span data-ttu-id="50be5-107">데이터베이스 처리량은 데이터베이스가 1초 이내에 수행할 수 있는 읽기 및 쓰기 수입니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-107">Database throughput is the number of reads and writes that your database can perform in a single second.</span></span> 

<span data-ttu-id="50be5-108">처리량 크기를 전략적으로 조정하려면 다양한 시간 및 다양한 문서 크기로 지원해야 하는 읽기 및 쓰기 수를 예측하여 처리량 요구 사항을 예측해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-108">To scale throughput strategically, you need to estimate your throughput needs by estimating the number of reads and writes you'll have to support at different times and for different document sizes.</span></span> <span data-ttu-id="50be5-109">정확하게 예측하면 수요가 급증할 때 사용자를 만족하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-109">If you estimate correctly, you'll keep your users happy when demand spikes.</span></span> <span data-ttu-id="50be5-110">정확하지 않게 예측하면 요청 속도가 제한되고 작업이 대기하고 다시 시도해야 하므로 대기 시간이 길어지고 고객이 만족하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-110">If you estimate incorrectly, your requests can get rate-limited and operations will have to wait and retry, likely causing high latency and unhappy customers.</span></span>

## <a name="what-is-a-request-unit"></a><span data-ttu-id="50be5-111">요청 단위란?</span><span class="sxs-lookup"><span data-stu-id="50be5-111">What is a request unit?</span></span>

<span data-ttu-id="50be5-112">Azure Cosmos DB는 **RU(요청 단위)** 라는 항목을 사용하여 처리량을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-112">Azure Cosmos DB measures throughput using something called a **request unit (RU)**.</span></span> <span data-ttu-id="50be5-113">요청 단위 사용량은 초당 측정되므로 측정 단위는 **RU/s(초당 요청 단위)** 입니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-113">Request unit usage is measured per second, so the unit of measure is **request units per second (RU/s)**.</span></span> <span data-ttu-id="50be5-114">Azure Cosmos DB에서 미리 프로비전할 RU/s 수를 예약해야 하므로, 예측한 로드를 처리할 수 있고 언제든지 현재 수요를 충족하도록 RU/s를 강화하거나 규모를 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-114">You must reserve the number of RU/s you want Azure Cosmos DB to provision in advance, so it can handle the load you've estimated, and you can scale your RU/s up or down at any time to meet current demand.</span></span>

## <a name="request-unit-basics"></a><span data-ttu-id="50be5-115">요청 단위 기본 사항</span><span class="sxs-lookup"><span data-stu-id="50be5-115">Request unit basics</span></span>

<span data-ttu-id="50be5-116">단일 요청 단위인 1 RU는 문서 ID를 사용하여 1KB 문서에서 단일 GET 요청을 실행하는 대략적인 비용과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-116">A single request unit, 1 RU, is equal to the approximate cost of performing a single GET request on a 1-KB document using a document's ID.</span></span> <span data-ttu-id="50be5-117">문서 ID를 사용하여 GET을 실행하는 기능은 문서를 검색하는 효율적인 수단이므로 비용이 적습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-117">Performing a GET by using a document's ID is an efficient means for retrieving a document, and thus the cost is small.</span></span> <span data-ttu-id="50be5-118">동일한 항목을 만들거나, 바꾸거나, 삭제하려면 서비스에 의한 추가 처리가 필요하므로 더 많은 요청 단위가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-118">Creating, replacing, or deleting the same item requires additional processing by the service, and therefore requires more request units.</span></span>

<span data-ttu-id="50be5-119">문서 크기, 문서의 속성 수, 수행 중인 작업 및 일부 추가 복합 개념(예: 일관성 및 인덱싱 정책)에 따라 작업 변경에 사용되는 요청 단위 수입니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-119">The number of request units used for an operation changes depending on the document size, the number of properties in the document, the operation being performed, and some additional complex concepts such as consistency and indexing policy.</span></span>

<span data-ttu-id="50be5-120">다음 표는 세 가지 크기(1KB, 4KB 및 64KB)와 두 가지 다른 성능 수준(500 읽기/초 + 100 쓰기/초 및 500 읽기/초 + 500 쓰기/초)의 항목에 필요한 요청 단위 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-120">The following table shows the number of request units required for items of three different sizes (1 KB, 4 KB, and 64 KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="50be5-121">이 예제에서 데이터 일관성은 **세션**으로 설정되었으며 인덱싱 정책은 **None**으로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-121">In this example, the data consistency is set to **Session**, and the indexing policy is set to **None**.</span></span>

| <span data-ttu-id="50be5-122">항목 크기</span><span class="sxs-lookup"><span data-stu-id="50be5-122">Item size</span></span> | <span data-ttu-id="50be5-123">읽기/초</span><span class="sxs-lookup"><span data-stu-id="50be5-123">Reads/second</span></span> | <span data-ttu-id="50be5-124">쓰기/초</span><span class="sxs-lookup"><span data-stu-id="50be5-124">Writes/second</span></span> | <span data-ttu-id="50be5-125">요청 단위</span><span class="sxs-lookup"><span data-stu-id="50be5-125">Request units</span></span>
| --- | --- | --- | --- |
| <span data-ttu-id="50be5-126">1KB</span><span class="sxs-lookup"><span data-stu-id="50be5-126">1 KB</span></span> | <span data-ttu-id="50be5-127">500</span><span class="sxs-lookup"><span data-stu-id="50be5-127">500</span></span> | <span data-ttu-id="50be5-128">100</span><span class="sxs-lookup"><span data-stu-id="50be5-128">100</span></span> | <span data-ttu-id="50be5-129">(500 * 1) + (100 * 5) = 1,000RU/s</span><span class="sxs-lookup"><span data-stu-id="50be5-129">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span>
| <span data-ttu-id="50be5-130">1KB</span><span class="sxs-lookup"><span data-stu-id="50be5-130">1 KB</span></span> | <span data-ttu-id="50be5-131">500</span><span class="sxs-lookup"><span data-stu-id="50be5-131">500</span></span> | <span data-ttu-id="50be5-132">500</span><span class="sxs-lookup"><span data-stu-id="50be5-132">500</span></span> | <span data-ttu-id="50be5-133">(500 * 1) + (500 * 5) = 3,000RU/s</span><span class="sxs-lookup"><span data-stu-id="50be5-133">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span>
| <span data-ttu-id="50be5-134">4KB</span><span class="sxs-lookup"><span data-stu-id="50be5-134">4 KB</span></span> | <span data-ttu-id="50be5-135">500</span><span class="sxs-lookup"><span data-stu-id="50be5-135">500</span></span> | <span data-ttu-id="50be5-136">100</span><span class="sxs-lookup"><span data-stu-id="50be5-136">100</span></span> | <span data-ttu-id="50be5-137">(500 * 1.3) + (100 * 7) = 1,350RU/s</span><span class="sxs-lookup"><span data-stu-id="50be5-137">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span>
| <span data-ttu-id="50be5-138">4KB</span><span class="sxs-lookup"><span data-stu-id="50be5-138">4 KB</span></span> | <span data-ttu-id="50be5-139">500</span><span class="sxs-lookup"><span data-stu-id="50be5-139">500</span></span> | <span data-ttu-id="50be5-140">500</span><span class="sxs-lookup"><span data-stu-id="50be5-140">500</span></span> | <span data-ttu-id="50be5-141">(500 * 1.3) + (500 * 7) = 4,150RU/s</span><span class="sxs-lookup"><span data-stu-id="50be5-141">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span>
| <span data-ttu-id="50be5-142">64KB</span><span class="sxs-lookup"><span data-stu-id="50be5-142">64 KB</span></span> | <span data-ttu-id="50be5-143">500</span><span class="sxs-lookup"><span data-stu-id="50be5-143">500</span></span> | <span data-ttu-id="50be5-144">100</span><span class="sxs-lookup"><span data-stu-id="50be5-144">100</span></span> | <span data-ttu-id="50be5-145">(500 * 10) + (100 * 48) = 9,800RU/s</span><span class="sxs-lookup"><span data-stu-id="50be5-145">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span>
| <span data-ttu-id="50be5-146">64KB</span><span class="sxs-lookup"><span data-stu-id="50be5-146">64 KB</span></span> | <span data-ttu-id="50be5-147">500</span><span class="sxs-lookup"><span data-stu-id="50be5-147">500</span></span> | <span data-ttu-id="50be5-148">500</span><span class="sxs-lookup"><span data-stu-id="50be5-148">500</span></span> | <span data-ttu-id="50be5-149">(500 * 10) + (500 * 48) = 29,000RU/s</span><span class="sxs-lookup"><span data-stu-id="50be5-149">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span>
 
<span data-ttu-id="50be5-150">확인할 수 있는 것처럼 항목이 크고 필요한 읽기 및 쓰기가 더 많을수록 예약해야 하는 요청 단위가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-150">As you can see, the larger the item is, and the more reads and writes are required, the more request units you need to reserve.</span></span> <span data-ttu-id="50be5-151">응용 프로그램의 처리량 요구 사항을 예측해야 하는 경우 Azure Cosmos DB [Capacity Planner](https://www.documentdb.com/capacityplanner)는 샘플 JSON 문서를 업로드하고 초당 완료해야 하는 작업 수를 설정할 수 있는 온라인 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-151">If you need to estimate the throughput needs of an application, the Azure Cosmos DB [Capacity Planner](https://www.documentdb.com/capacityplanner) is an online tool that enables you to upload a sample JSON document and set the number of operations you need to complete per second.</span></span> <span data-ttu-id="50be5-152">이 도구는 예약할 예측된 합계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-152">It then provides an estimated total to reserve.</span></span>

## <a name="exceeding-throughput-limits"></a><span data-ttu-id="50be5-153">처리량 한도 초과</span><span class="sxs-lookup"><span data-stu-id="50be5-153">Exceeding throughput limits</span></span>

<span data-ttu-id="50be5-154">충분한 요청 단위를 예약하지 않고 프로비전된 처리량보다 많은 데이터를 읽거나 쓰려고 하면 요청 속도가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-154">If you don’t reserve enough request units, and you attempt to read or write more data than your provisioned throughput allows, your request will be rate-limited.</span></span> <span data-ttu-id="50be5-155">요청 속도가 제한되면 지정된 간격 후에 요청을 다시 시도해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-155">When a request is rate-limited, the request has to be retried again after a specified interval.</span></span> <span data-ttu-id="50be5-156">.NET SDK를 사용하는 경우 retry-after 헤더에 지정된 시간을 대기한 후 요청이 자동으로 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-156">If you use the .NET SDK, the request will be retried automatically after waiting the amount of time specified in the retry-after header.</span></span>

## <a name="creating-an-account-built-to-scale"></a><span data-ttu-id="50be5-157">크기를 조정하도록 빌드된 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="50be5-157">Creating an account built to scale</span></span>

<span data-ttu-id="50be5-158">언제든지 데이터베이스에 프로비전된 요청 단위 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-158">You can change the number of request units provisioned to a database at any time.</span></span> <span data-ttu-id="50be5-159">따라서 처리량이 많은 기간에는 이렇게 높은 수요를 수용하도록 확장하고, 처리량이 적은 기간에는 프로비전된 처리량을 줄여 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-159">So, during heavy volume periods, you can scale up to accommodate those high demands, and then reduce provisioned throughput during off peak times to reduce costs.</span></span>

<span data-ttu-id="50be5-160">계정을 만들 때 포털에서 최소 400RU/s 또는 최대 250,000RU/s를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-160">When you create an account, you can provision a minimum of 400 RU/s, or a maximum of 250,000 RU/s in the portal.</span></span> <span data-ttu-id="50be5-161">훨씬 더 많은 처리량이 필요한 경우에는 Azure Portal에서 티켓을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-161">If you need even more throughput, fill out a ticket in the Azure portal.</span></span> <span data-ttu-id="50be5-162">거의 모든 계정에서 초기 처리량을 1000RU/s로 설정하는 것이 좋습니다. 이 값은 10GB보다 큰 저장소가 필요한 경우 데이터베이스가 자동으로 크기를 조정할 최소값입니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-162">Setting the initial throughput to 1000 RU/s is recommended for almost all accounts, as it is the minimum value in which your database will autoscale should you need more than 10 GB of storage.</span></span> <span data-ttu-id="50be5-163">초기 처리량을 1000RU/s보다 적은 값으로 설정하면 데이터베이스가 10GB보다 크게 확장될 수 없습니다. 단, 데이터베이스를 다시 프로비전하고 파티션 키를 제공하면 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-163">If you set the initial throughput to any value less than 1000 RU/s, your database will not be able to scale to larger than 10 GB unless you reprovision the database and provide a partition key.</span></span> <span data-ttu-id="50be5-164">파티션 키를 사용하면 Azure Cosmos DB에서 데이터를 빠르게 조회할 수 있고 필요한 경우 데이터베이스의 크기를 자동으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-164">Partition keys enable quick lookup of data in Azure Cosmos DB and enable it to autoscale your database when needed.</span></span> <span data-ttu-id="50be5-165">파티션 키는 다음 단원에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-165">Partition keys are discussed in the next unit.</span></span>

## <a name="summary"></a><span data-ttu-id="50be5-166">요약</span><span class="sxs-lookup"><span data-stu-id="50be5-166">Summary</span></span>

<span data-ttu-id="50be5-167">이제 요청 단위를 사용하여 Azure Cosmos DB에 대한 처리량을 예측하고 범위를 지정하는 방법을 이해하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-167">You now understand how to estimate and scope throughput for an Azure Cosmos DB using request units.</span></span> <span data-ttu-id="50be5-168">요청 단위는 언제든지 수정할 수 있으며, 계정을 만들 때 1000RU/s로 설정하면 나중에 데이터베이스가 크기를 조정할 준비가 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50be5-168">Request units can be modified at any time, and setting them to 1000 RU/s when you create an account helps ensure your database is ready to scale later.</span></span>