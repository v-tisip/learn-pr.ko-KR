<span data-ttu-id="c31eb-101">음악 공유 응용 프로그램의 아키텍처를 계획한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-101">Suppose you are planning the architecture for your music-sharing application.</span></span> <span data-ttu-id="c31eb-102">모바일 앱에서 웹 API에 음악 파일이 안정적으로 업로드되는지 확인하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-102">You want to choose ensure that music files are uploaded to the web API reliably from the mobile app.</span></span>

<span data-ttu-id="c31eb-103">이 통신이 메시지인 것을 확인했으므로 Azure Storage 큐 또는 Service Bus를 사용할지 여부를 선택해야 합니다. 이러한 서비스는 둘 다 처리를 기다릴 때 메시지 큐를 저장하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-103">Having understood that this communication should be a message, you must choose whether to use Azure Storage queues or Service Bus, both of which can be used to store queues of messages as they await processing.</span></span>

## <a name="delivery-guarantees"></a><span data-ttu-id="c31eb-104">전송 보장</span><span class="sxs-lookup"><span data-stu-id="c31eb-104">Delivery Guarantees</span></span>

<span data-ttu-id="c31eb-105">큐 시스템은 일반적으로 큐의 각 메시지를 대상 구성 요소에 전송하도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-105">Queuing systems usually guarantee delivery of each message in the queue to a destination component.</span></span> <span data-ttu-id="c31eb-106">그러나 이러한 보장에는 다음과 같은 다양한 방법이 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-106">However, these guarantees can take different approaches:</span></span>

- <span data-ttu-id="c31eb-107">**최소 1회(At-Least-Once) 전송.**</span><span class="sxs-lookup"><span data-stu-id="c31eb-107">**At-Least-Once Delivery.**</span></span> <span data-ttu-id="c31eb-108">이 방법에서 각 메시지는 큐에서 메시지를 검색하는 하나 이상의 구성 요소에 전송되도록 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-108">In this approach, each message is guaranteed to be delivered to at least one of the components that retrieve messages from the queue.</span></span> <span data-ttu-id="c31eb-109">그러나 특정 상황에서는 동일한 메시지가 두 번 이상 전송될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-109">Note, however, that in certain circumstances, it is possible that the same message may be delivered more than once.</span></span> <span data-ttu-id="c31eb-110">예를 들어 큐에서 메시지를 검색하는 웹앱의 두 인스턴스가 있는 경우 일반적으로 각 메시지는 해당 인스턴스 중 하나로만 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-110">For example, if there are two instances of a web app retrieving messages from a queue, ordinarily each message goes to only one of those instances.</span></span> <span data-ttu-id="c31eb-111">그러나 한 인스턴스가 메시지를 처리하는 데 시간이 오래 걸리고 시간 제한이 만료되면 메시지가 다른 인스턴스에도 전송될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-111">However, if one instance takes a long time to process the message, and a time-out expires, the message may be sent to the other instance as well.</span></span> <span data-ttu-id="c31eb-112">웹앱 코드는 이 가능성을 염두에 두고 디자인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-112">Your web app code should be designed with this possibility in mind.</span></span>
- <span data-ttu-id="c31eb-113">**최대 1회(At-Most-Once) 전송.**</span><span class="sxs-lookup"><span data-stu-id="c31eb-113">**At-Most-Once Delivery.**</span></span> <span data-ttu-id="c31eb-114">이 방법에서 각 메시지는 전송되도록 보장되지 않고 도착하지 않을 가능성이 매우 적습니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-114">In this approach, each message is not guaranteed to be delivered and there is a very small chance that it may not arrive.</span></span> <span data-ttu-id="c31eb-115">그러나 메시지가 최소 1회(At-Least-Once) 전송과 같이 두 번 전송될 가능성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-115">However, there is no chance that the message will be delivered twice as with At-Least-Once delivery.</span></span>
- <span data-ttu-id="c31eb-116">**FIFO(선입 선출).**</span><span class="sxs-lookup"><span data-stu-id="c31eb-116">**First-In-First-Out (FIFO).**</span></span> <span data-ttu-id="c31eb-117">대부분의 메시징 시스템에서 메시지는 일반적으로 추가된 동일한 순서로 큐를 떠나지만 이 순서를 보장할지 여부를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-117">In most messaging system, messages usually leave the queue in the same order in which they were added but you should consider whether this order is guaranteed.</span></span> <span data-ttu-id="c31eb-118">배포 응용 프로그램에서 메시지를 올바른 순서로 정확하게 처리해야 하는 경우, FIFO 보장을 포함하는 큐 시스템을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-118">If your distributed application requires that messages are processed in precisely the correct order, you must choose a queue system that includes a FIFO guarantee.</span></span>

## <a name="transactions"></a><span data-ttu-id="c31eb-119">트랜잭션</span><span class="sxs-lookup"><span data-stu-id="c31eb-119">Transactions</span></span>

<span data-ttu-id="c31eb-120">그룹의 한 메시지에 대한 전송이 실패하면 일부 밀접하게 관련된 메시지 그룹으로 인해 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-120">Some closely related groups of messages may cause problems when delivery fails for one message in the group.</span></span>

<span data-ttu-id="c31eb-121">예를 들어 전자상거래 응용 프로그램을 생각해 보세요.</span><span class="sxs-lookup"><span data-stu-id="c31eb-121">For example, consider an e-commerce application.</span></span> <span data-ttu-id="c31eb-122">사용자가 “구입” 단추를 클릭하면 주문 정보가 포함된 메시지가 신용 카드 정보가 포함된 메시지와 함께 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-122">When the user clicks the "Buy" button, a message with the order details is sent along with a message with the credit card details.</span></span> <span data-ttu-id="c31eb-123">신용 카드 메시지가 전송되지 않으면 주문이 결제 없이 발송될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-123">If the credit card message is not delivered, the order may be dispatched without payment.</span></span>

<span data-ttu-id="c31eb-124">두 메시지를 한 트랜잭션으로 그룹화하여 이런 종류의 문제점을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-124">You can avoid these kinds of problems by grouping the two messages into a transaction.</span></span> <span data-ttu-id="c31eb-125">트랜잭션이 하나의 단위로 성공하거나 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-125">Transactions succeed or fail as a single unit.</span></span> <span data-ttu-id="c31eb-126">신용 카드 정보 메시지 전송이 실패하면 주문 정보 메시지 전송도 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-126">If the credit card details message delivery fails then so will the order details message.</span></span>

## <a name="when-to-use-storage-queues"></a><span data-ttu-id="c31eb-127">Storage 큐를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="c31eb-127">When to use Storage queues</span></span>

<span data-ttu-id="c31eb-128">큐는 메시지에 사용되지만 이벤트는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-128">Queues are used for messages but not events.</span></span>

<span data-ttu-id="c31eb-129">Azure Storage 계정에는 배포 응용 프로그램에서 메시지의 단순 임시 저장소 위치로 사용할 수 있는 큐가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-129">Azure Storage Accounts include queues, which can be used by distributed applications as simple temporary storage locations for messages.</span></span> <span data-ttu-id="c31eb-130">원본 구성 요소는 큐에 메시지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-130">A source component can add a message to the queue.</span></span> <span data-ttu-id="c31eb-131">대상 구성 요소는 처리를 위해 큐의 앞에서 메시지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-131">Destination components retrieve the message at the front of the queue for processing.</span></span> <span data-ttu-id="c31eb-132">수요가 많을 경우 대상 구성 요소가 처리 준비를 완료할 때까지 메시지가 단순히 대기할 수 있기 때문에 이러한 큐는 메시지 교환의 안정성을 높입니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-132">Such queues increase the reliability of the message exchange because, at times of high demand, messages can simply wait until a destination component is ready to process them.</span></span>

<span data-ttu-id="c31eb-133">큐는 Azure Service Bus 메시징의 일부로도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-133">Queues are also provided as part of Azure Service Bus Messaging.</span></span> <span data-ttu-id="c31eb-134">특정 통신에 Azure의 큐를 사용하기로 한 경우 Storage 큐 또는 Service Bus 큐를 사용할지 여부를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-134">If you have decided to use a queue in Azure for a specific communication, you must decide whether to use a Storage queue or a Service Bus queue.</span></span>

<span data-ttu-id="c31eb-135">이 항목을 선택하려면 다음 질문을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="c31eb-135">To make this choice, consider the following questions:</span></span>

- <span data-ttu-id="c31eb-136">최대 1회(At-Most-Once) 전송 보장이 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="c31eb-136">Do you need an At-Most-Once delivery guarantee?</span></span>
- <span data-ttu-id="c31eb-137">FIFO 보장이 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="c31eb-137">Do you need a FIFO guarantee?</span></span>
- <span data-ttu-id="c31eb-138">메시지를 트랜잭션으로 그룹화해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="c31eb-138">Do you need to group messages into transactions?</span></span>
- <span data-ttu-id="c31eb-139">64KB를 초과하는 메시지를 저장해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="c31eb-139">Do you need to store messages larger than 64KB?</span></span>

<span data-ttu-id="c31eb-140">이러한 질문에 예를 선택하면 Service Bus 큐를 사용하도록 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-140">If the answer to any of these questions is yes, you must choose to use a Service Bus queue.</span></span>

<span data-ttu-id="c31eb-141">또한 다음을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="c31eb-141">In addition consider:</span></span>

- <span data-ttu-id="c31eb-142">큐를 통과하는 모든 메시지의 서버 쪽 로그가 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="c31eb-142">Do you need server-side logs of all messages that pass through the queue?</span></span>
- <span data-ttu-id="c31eb-143">큐의 크기가 80GB를 초과할 것으로 예상하나요?</span><span class="sxs-lookup"><span data-stu-id="c31eb-143">Do you expect the queue to exceed 80GB in size?</span></span>

<span data-ttu-id="c31eb-144">이러한 질문에 예를 선택하면 Storage 큐를 사용하도록 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-144">If the answer to any of these questions is yes, you must choose to use a Storage queue.</span></span>

## <a name="summary"></a><span data-ttu-id="c31eb-145">요약</span><span class="sxs-lookup"><span data-stu-id="c31eb-145">Summary</span></span>

<span data-ttu-id="c31eb-146">큐는 배포 응용 프로그램의 구성 요소 간에 전송되는 메시지에 대한 단순 임시 저장소 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-146">A queue is a simple temporary storage location for messages sent between the components of a distributed application.</span></span> <span data-ttu-id="c31eb-147">큐를 사용하여 메시지를 구성하고 필요에 따라 예기치 않은 서지를 정상적으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-147">Use a queue to organize message and gracefully handle unpredictable surges in demand.</span></span>

<span data-ttu-id="c31eb-148">단순 및 코딩하기 쉬운 큐 시스템을 원하는 경우 Azure Storage 큐를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-148">Use Azure Storage queues when you want a simple and easy-to-code queue system.</span></span> <span data-ttu-id="c31eb-149">더 높은 수준의 요구 사항에는 Azure Service Bus 큐를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c31eb-149">For more advanced needs, use Azure Service Bus queues.</span></span>