<span data-ttu-id="f9ac2-101">온도 데이터 서비스를 생성하기 전에 서버리스 계산이 작업에 가장 좋은 솔루션인지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-101">Before you create your temperature data service, you want to ensure serverless compute is the best solution for the job.</span></span> 

## <a name="what-is-serverless-compute"></a><span data-ttu-id="f9ac2-102">서버리스 계산이란?</span><span class="sxs-lookup"><span data-stu-id="f9ac2-102">What is serverless compute?</span></span>
<span data-ttu-id="f9ac2-103">서버리스 계산은 FaaS(Function as a Service) 또는 클라우드 플랫폼에서 호스트되는 마이크로 서비스로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-103">Serverless compute can be thought of as a function as a service (FaaS), or a microservice that is hosted on a cloud platform.</span></span> <span data-ttu-id="f9ac2-104">이 함수에는 인프라를 수동으로 프로비전하거나 확장하지 않고 실행할 수 있는 비즈니스 논리 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-104">This function contains business logic code that can be executed without manually provisioning or scaling infrastructure.</span></span> <span data-ttu-id="f9ac2-105">호스팅 플랫폼은 추상화되므로, 직접 액세스할 수 있는 서버가 없으며 추산할 크기 조정이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-105">The hosting platform is abstracted; there are no servers to access directly and no scaling to estimate.</span></span> 

## <a name="what-is-azure-functions"></a><span data-ttu-id="f9ac2-106">Azure Functions란?</span><span class="sxs-lookup"><span data-stu-id="f9ac2-106">What is Azure Functions?</span></span>
<span data-ttu-id="f9ac2-107">Azure Functions는 서버리스 응용 프로그램 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-107">Azure Functions is a serverless application platform.</span></span> <span data-ttu-id="f9ac2-108">이를 통해 개발자는 인프라를 프로비전하지 않고도 실행할 수 있는 비즈니스 논리를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-108">It allows developers to host business logic that can be executed without provisioning infrastructure.</span></span> <span data-ttu-id="f9ac2-109">Azure Functions는 기본적으로 확장성을 제공하고 사용된 리소스에 대한 요금만 부과합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-109">Azure Functions provides intrinsic scalability and bills only for the resources used.</span></span> <span data-ttu-id="f9ac2-110">Azure Functions는 C#, F#, JavaScript 등의 다양한 언어로 코딩할 수 있으며 NuGet 및 NPM에 대한 지원을 제공하므로 많이 사용되는 다양한 라이브러리를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-110">Azure Functions can be coded in a variety of languages, including C#, F#, and JavaScript, and provides support for NuGet and NPM, so you can include many popular libraries.</span></span> 

## <a name="when-do-you-use-serverless-compute"></a><span data-ttu-id="f9ac2-111">서버리스 계산은 언제 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="f9ac2-111">When do you use serverless compute?</span></span>
<span data-ttu-id="f9ac2-112">서버리스 계산은 클라우드에서 비즈니스 논리 코드를 호스트하는 훌륭한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-112">Serverless compute is a great option for hosting business logic code in the cloud.</span></span> <span data-ttu-id="f9ac2-113">자동 크기 조정이 이루어지고, 관리할 서버가 없으며, 청구를 처리하는 데 1초도 걸리지 않고, 구현을 위해 여러 프로그래밍 언어를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-113">It has automatic scaling, no servers to manage, and subsecond billing, and provides a choice of multiple programming languages for implementation.</span></span> <span data-ttu-id="f9ac2-114">다음은 서버리스 계산으로 제공되는 몇 가지 추가적인 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-114">Here are some additional characteristics that are well served with serverless compute.</span></span>

### <a name="avoid-overallocation-of-infrastructure"></a><span data-ttu-id="f9ac2-115">인프라 초과 할당 없음</span><span class="sxs-lookup"><span data-stu-id="f9ac2-115">Avoid overallocation of infrastructure</span></span>
<span data-ttu-id="f9ac2-116">VM 서버를 프로비전하고 최고 로드 시간을 처리하기에 충분한 리소스로 구성했다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-116">Suppose you've provisioned VM servers and configured them with enough resources to handle your peak load times.</span></span> <span data-ttu-id="f9ac2-117">로드가 적은 경우에는 사용하지 않는 인프라에 대해 요금을 지불할 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-117">When load is light, you could potentially be paying for infrastructure you're not using.</span></span> <span data-ttu-id="f9ac2-118">서버리스 계산은 자동으로 크기를 확장 및 축소하여 초과 할당 문제를 해결하는 데 유용하며, 함수를 실행할 때만 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-118">Serverless compute helps solve the overallocation problem by scaling up or down automatically, and you're only billed when your function is running.</span></span>

### <a name="stateless-logic"></a><span data-ttu-id="f9ac2-119">상태 비저장 논리</span><span class="sxs-lookup"><span data-stu-id="f9ac2-119">Stateless logic</span></span>
<span data-ttu-id="f9ac2-120">상태 비저장 함수는 서버리스 계산을 위한 좋은 후보입니다. 함수 인스턴스는 요청 시 생성되고 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-120">Stateless functions are great candidates for serverless compute; function instances are created and destroyed on demand.</span></span> <span data-ttu-id="f9ac2-121">상태가 필요한 경우 연관된 저장소 서비스에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-121">If state is required, it can be stored in an associated storage service.</span></span>

### <a name="event-driven"></a><span data-ttu-id="f9ac2-122">이벤트 기반</span><span class="sxs-lookup"><span data-stu-id="f9ac2-122">Event driven</span></span>
<span data-ttu-id="f9ac2-123">Azure 함수는 이벤트 기반이며, HTTP 요청 또는 큐에 메시지 추가 등의 이벤트에 응답해서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-123">Azure functions are event driven; they run only in response to an event, such as receiving an HTTP request or a message being added to a queue.</span></span> <span data-ttu-id="f9ac2-124">Azure 함수 구성은 데이터가 들어오는 위치(트리거/입력 바인딩) 및 나가는 위치(출력 바인딩)를 선언할 수 있게 함으로써 코드베이스를 크게 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-124">Azure function configuration greatly simplifies your codebase by allowing you to declare where the data comes from (trigger/input binding) and where it goes (output binding).</span></span> <span data-ttu-id="f9ac2-125">큐, Blob, 허브 등을 보기 위한 쓰기 코드가 필요하지 않습니다. 비즈니스 논리에 전적으로 초점을 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-125">You don't need write code to watch queues, blobs, hubs, etc. You focus purely on the business logic.</span></span>

## <a name="when-do-you-not-use-serverless-compute"></a><span data-ttu-id="f9ac2-126">서버리스 계산을 사용하지 않는 경우는 언제인가요?</span><span class="sxs-lookup"><span data-stu-id="f9ac2-126">When do you not use serverless compute?</span></span>
<span data-ttu-id="f9ac2-127">서버리스 계산은 비즈니스 논리를 호스트하는 데 항상 적절한 솔루션이 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-127">Serverless compute will not always be the appropriate solution to hosting your business logic.</span></span> <span data-ttu-id="f9ac2-128">다음은 서버리스 계산으로 서비스를 호스트하기 위한 의사 결정에 영향을 줄 수 있는 Azure 함수의 몇 가지 특징입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-128">Here are a few characteristics of Azure functions that may affect your decision to host your services in serverless compute.</span></span> 

### <a name="execution-time"></a><span data-ttu-id="f9ac2-129">실행 시간</span><span class="sxs-lookup"><span data-stu-id="f9ac2-129">Execution time</span></span>
<span data-ttu-id="f9ac2-130">기본적으로 Azure 함수에는 5분의 제한 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-130">By default, Azure functions have a timeout of 5 minutes.</span></span> <span data-ttu-id="f9ac2-131">이를 최대 10분으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-131">This is configurable to a maximum of 10 minutes.</span></span> <span data-ttu-id="f9ac2-132">실행하는 데 10분 넘게 필요한 경우 VM에서 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-132">If your function requires more than 10 minutes to execute, you can host it on a VM.</span></span> <span data-ttu-id="f9ac2-133">그뿐만 아니라 HTTP 요청을 통해 서비스가 시작되고 해당 값이 HTTP 응답으로 예상되는 경우 제한 시간은 2.5분으로 더 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-133">Additionally, if your service is initiated through an HTTP request and you expect that value as an HTTP response, the timeout is further restricted to 2.5 minutes.</span></span>

### <a name="execution-frequency"></a><span data-ttu-id="f9ac2-134">실행 빈도</span><span class="sxs-lookup"><span data-stu-id="f9ac2-134">Execution frequency</span></span>
<span data-ttu-id="f9ac2-135">두 번째 특성은 실행 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-135">The second characteristic is execution frequency.</span></span> <span data-ttu-id="f9ac2-136">여러 클라이언트가 함수를 계속 실행할 것으로 예상되는 경우에는 사용을 추정하고 적절하게 Azure 함수 사용 비용을 계산하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-136">If you expect your function to be executed continuously by multiple clients, it would be prudent to estimate the usage and calculate the cost of using Azure functions accordingly.</span></span> <span data-ttu-id="f9ac2-137">VM에서 서비스를 호스트하는 것이 훨씬 더 저렴할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-137">It could very well be cheaper to host your service on a VM.</span></span>

<span data-ttu-id="f9ac2-138">크기가 조정되는 동안 10초마다 하나의 함수 앱 인스턴스만, 최대 총 200개의 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-138">While scaling, only one function app instance can be created every 10 seconds, for up to 200 total instances.</span></span> <span data-ttu-id="f9ac2-139">각 인스턴스는 여러 동시 실행을 서비스할 수 있으므로, 단일 인스턴스가 처리할 수 있는 트래픽의 양에는 일정한 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-139">Keep in mind, each instance has the ability to service multiple concurrent executions, so there is no set limit on how much traffic a single instance can handle.</span></span> <span data-ttu-id="f9ac2-140">서로 다른 유형의 트리거는 크기 조정 요구 사항이 서로 다르므로, 선택한 트리거를 알아보고 한도를 조사하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ac2-140">Different types of triggers have different scaling requirements, so research your choice of trigger and investigate its limits.</span></span>