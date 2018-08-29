<span data-ttu-id="5b430-101">이제 온도 서비스 구현을 시작할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-101">You are now ready to start implementing the temperature service.</span></span> <span data-ttu-id="5b430-102">이전 단원에서 요구 사항에 서버리스 솔루션이 가장 적절한지 판단했습니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-102">In the previous unit, you determined that a serverless solution would best fit your needs.</span></span> <span data-ttu-id="5b430-103">서버리스 Azure 함수를 구현하려면 “홈을 호출”하는 위치가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-103">To implement a serverless Azure function, it must have a place to "call home."</span></span> <span data-ttu-id="5b430-104">이 “홈”은 Azure 함수 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-104">This "home" is an Azure function app.</span></span>

## <a name="azure-function-app-overview"></a><span data-ttu-id="5b430-105">Azure 함수 앱 개요</span><span class="sxs-lookup"><span data-stu-id="5b430-105">Azure function app overview</span></span>
<span data-ttu-id="5b430-106">Azure 함수는 함수 앱이라고 하는 컨테이너에서 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-106">Azure functions are hosted in a container called a function app.</span></span> <span data-ttu-id="5b430-107">Azure에서 함수 앱을 정의하여 함수를 논리적으로 그룹화하고 구조화합니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-107">You define function apps in Azure to logically group and structure your functions.</span></span> <span data-ttu-id="5b430-108">함수 앱은 Azure의 계산 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-108">Function apps are a compute resource in Azure.</span></span> <span data-ttu-id="5b430-109">엘리베이터 예에서, 에스컬레이터 드라이브 기어 온도 서비스를 호스트하는 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-109">In our elevator example, you would create a function app to host the escalator drive gear temperature service.</span></span> <span data-ttu-id="5b430-110">함수 앱을 만들려면 몇 가지 결정해야 할 일이 있습니다. 서비스 계획을 선택하고, 호환되는 저장소 계정을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-110">There are a few decisions that need to be made in order to create the function app; you need to choose a service plan, and select a compatible storage account.</span></span>

### <a name="choosing-a-service-plan"></a><span data-ttu-id="5b430-111">서비스 계획 선택</span><span class="sxs-lookup"><span data-stu-id="5b430-111">Choosing a service plan</span></span>
<span data-ttu-id="5b430-112">함수 앱은 두 가지 유형의 서비스 계획 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-112">Function apps may use one of two types of service plans.</span></span> <span data-ttu-id="5b430-113">첫 번째 서비스 계획은 소비 서비스 계획으로,</span><span class="sxs-lookup"><span data-stu-id="5b430-113">The first service plan is the Consumption service plan.</span></span> <span data-ttu-id="5b430-114">Azure 서버리스 응용 프로그램 플랫폼을 사용할 때 선택하는 플랜입니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-114">This is the plan that you choose when using the Azure serverless application platform.</span></span> <span data-ttu-id="5b430-115">소비 서비스 계획은 자동 크기 조정을 제공하며 함수를 실행할 때 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-115">The Consumption service plan provides automatic scaling, and bills you when the functions are running.</span></span> <span data-ttu-id="5b430-116">소비 플랜에서는 함수 실행에 대해 구성 가능한 제한 시간이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-116">The Consumption plan comes with a configurable timeout period for the execution of a function.</span></span> <span data-ttu-id="5b430-117">기본적으로 5분이지만 제한 시간을 최대 10분까지 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-117">By default it is 5 minutes, but may be configured to have a timeout as long as 10 minutes.</span></span> 

<span data-ttu-id="5b430-118">두 번째 계획은 Azure App Service 계획이라고 하며,</span><span class="sxs-lookup"><span data-stu-id="5b430-118">The second plan is called the Azure App Service plan.</span></span> <span data-ttu-id="5b430-119">이를 통해 VM에서 함수를 지속적으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-119">This plan allows you to have your function run continuously on a VM.</span></span> <span data-ttu-id="5b430-120">함수가 지속적으로 사용되는 경우 또는 소비 플랜이 제공할 수 있는 것보다 더 많은 처리 능력이나 실행 시간이 필요한 경우 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-120">You would choose this option if your functions are used continuously or require more processing power or execution time than the Consumption plan can provide.</span></span> 

### <a name="storage-account-requirements"></a><span data-ttu-id="5b430-121">Storage 계정 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5b430-121">Storage account requirements</span></span>
<span data-ttu-id="5b430-122">함수 앱을 만들면 이 앱은 일반적으로 Azure Blob, Queue 및 Table Storage를 지원하는 저장소 계정에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-122">When you create a function app, it is typically linked to a storage account that supports Azure Blob, Queue, and Table storage.</span></span> <span data-ttu-id="5b430-123">함수 앱은 함수 실행 로깅 및 실행 트리거 관리 등과 같은 내부 작업을 위해 이 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-123">The function app uses this storage account for internal operations such as logging function executions and managing execution triggers.</span></span> <span data-ttu-id="5b430-124">또한 소비 서비스 계획의 경우 Azure 함수 코드 및 구성 파일이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b430-124">This is also where, on the Consumption service plan, the Azure function code and configuration files are stored.</span></span> 