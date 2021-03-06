Azure 제품은 여러 계층으로 이루어져 있습니다. 예를 들어 Linux 가상 머신을 만들어야 한다고 가정해 보겠습니다. **홈** **>** **가상 머신** **>** **계산** **>** **Ubuntu Server**와 같이 여러 수준에서 탐색할 수 있습니다. Azure Portal은 해당 UI를 최적화하여 이러한 유형의 탐색 시퀀스를 쉽게 이해할 수 있도록 합니다. 여기서는 이를 가능하게 하는 주요 UI 요소를 살펴보겠습니다. 메뉴 및 하위 메뉴를 탐색하고 블레이드를 사용하여 서비스를 찾아 구성합니다.

## <a name="azure-portal-layout"></a>Azure Portal 레이아웃

Azure Portal은 Microsoft Azure를 제어하기 위한 기본 GUI(그래픽 사용자 인터페이스)입니다. 포털에서는 대부분의 관리 작업을 수행할 수 있으며 포털은 일반적으로 단일 작업을 수행하거나 구성 옵션을 자세히 보기에 가장 적합한 인터페이스입니다.

포털의 왼쪽 창은 기본 리소스 종류가 나열된 리소스 창입니다. Azure의 리소스 종류는 표시된 것보다 훨씬 많습니다.

## <a name="using-blades-in-azure-portal"></a>Azure Portal에서 블레이드 사용

Azure Portal에서는 탐색을 위해 블레이드 모델을 사용합니다. _블레이드_는 탐색 시퀀스의 한 수준에 사용되는 UI가 포함된 슬라이드 아웃 패널입니다. 예를 들어 이 시퀀스의 각 요소는 **가상 머신** **>** **계산** **>** **Ubuntu Server**와 같은 블레이드로 표시됩니다.

UI 내 각 블레이드에는 일반적으로 여러 구성 가능한 옵션이 포함되어 있습니다. 이러한 옵션 중 일부는 기존 블레이드의 오른쪽에 자신을 표시하는 다른 블레이드를 생성합니다. 새 블레이드에서는 모든 추가 구성 가능한 옵션이 또 다른 블레이드를 생성하는 방식으로 수행됩니다. 금방 여러 블레이드가 동시에 열려 있는 상태가 될 수 있습니다. 블레이드를 최대화하여 전체 화면을 채울 수도 있습니다.

구성 변경을 수행하고 저장하지 않은 상태로 블레이드를 닫으려고 하면 메시지가 표시됩니다.

## <a name="configuring-settings-in-azure-portal"></a>Azure Portal에서 설정 구성

Azure Portal은 대개 화면의 오른쪽 맨 위에 있는 상태 표시줄에 여러 구성 옵션을 표시합니다.

### <a name="notifications"></a>공지

벨 아이콘을 클릭하면 알림 창이 표시됩니다. 이 창에는 수행한 마지막 작업이 해당 상태와 함께 나열됩니다.

![알림 블레이드](../images/2-notifications-blade.PNG)

### <a name="cloud-shell"></a>Cloud Shell

Cloud Shell 아이콘(>_)을 클릭하면 새 Cloud Shell 세션을 만듭니다. 해당 세션에서 Linux Bash 또는 Linux 기반 PowerShell을 사용하라는 메시지가 표시됩니다.

![Cloud Shell](../images/2-choose-shell.PNG)

### <a name="settings"></a>설정

Azure Portal 설정을 변경하려면 “기어” 아이콘을 클릭합니다. 이러한 설정에는 다음이 포함됩니다.

* 로그아웃 시간
* 색 구성표
* 고대비 테마
* 알림 메시지(모바일 장치 대상)
* 테마를 변경하려면 두 번 클릭
* 언어
* 사용지역 언어

![포털 설정](../images/2-settings-blade.PNG)

설정을 변경한 경우 **적용**을 클릭하여 변경을 수락합니다.

### <a name="feedback-blade"></a>피드백 블레이드

웃는 얼굴 아이콘은 **피드백 보내기** 블레이드를 엽니다. 여기에서 Azure에 대한 피드백을 Microsoft로 보낼 수 있습니다. Microsoft가 메일로 피드백에 응답할 수 있는지 여부를 지정할 수 있습니다.

![사용자 의견](../images/2-feedback-blade.PNG)

### <a name="help-blade"></a>도움말 블레이드

물음표를 클릭하여 **도움말** 블레이드를 표시합니다. 여기서 다음과 같은 여러 항목 중에서 선택할 수 있습니다.

* 새로운 기능
* Azure 로드맵
* 둘러보기 시작
* 바로 가기 키
* 진단 표시
* 개인정보처리방침

### <a name="directory-and-subscription"></a>디렉터리 및 구독

책 및 필터 아이콘을 클릭하여 **디렉터리 + 구독** 블레이드를 표시합니다.

Azure를 사용하면 두 개 이상의 구독을 하나의 디렉터리와 연결할 수 있습니다. 디렉터리 및 구독 블레이드에서는 구독 간에 변경할 수 있습니다. 여기서 구독을 변경하거나 다른 디렉터리로 변경할 수 있습니다.

![디렉터리](../images/2-directory-blade-1.PNG)

### <a name="profile-settings"></a>프로필 설정

오른쪽 위에 있는 이름을 클릭하면 프로필 설정을 변경할 수 있습니다.
옵션은 다음과 같습니다.

* Azure에서 로그아웃
* 암호 변경
* 연락처 정보 변경
* 권한 보기
* Azure 팀에 아이디어 제출
* 청구서 보기
* 디렉터리 전환(이전 섹션에서처럼 디렉터리 + 구독 블레이드 표시)

![프로필 설정](../images/2-portal-menu.png)

**청구서 보기**를 클릭하는 경우 **Cost Management + 청구 - 송장** 페이지로 이동하므로 Azure에서 비용이 발생하는 부분을 분석하는 데 도움이 됩니다.

![청구 페이지](../images/2-portal-billing.PNG)

## <a name="summary"></a>요약

Azure는 대규모 제품이며 포털 UI에는 이러한 특징이 잘 반영되어 있습니다. 포털에서 이렇게 복잡한 탐색을 지원하는 기본적인 방법은 블레이드를 통해 계층 구조를 나타내는 것입니다. 블레이드를 사용하면 특정 작업에 집중할 수 있을 뿐만 아니라 해당 위치에 도달하게 된 경로를 명확하게 보여 줍니다.