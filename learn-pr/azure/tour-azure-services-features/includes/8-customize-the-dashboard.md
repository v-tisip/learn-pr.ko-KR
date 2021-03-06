여기에서는 포털 UI를 사용하고 기본 JSON 파일을 직접 편집하여 대시보드를 만들고 수정합니다.

## <a name="what-is-a-dashboard"></a>대시보드란 무엇인가요?

_대시보드_는 Azure Portal에 표시되는 사용자 지정 가능한 UI 타일 컬렉션입니다. 타일을 추가, 제거 및 배치하여 원하는 뷰를 만들고 해당 뷰를 대시보드로 저장합니다. 여러 대시보드가 지원되며 필요에 따라 대시보드 간에 전환할 수 있습니다. 다른 팀 구성원과 대시보드를 공유할 수도 있습니다.

대시보드는 Azure 관리 방법 측면에서 상당한 유연성을 제공합니다. 예를 들어 조직 내의 특정 역할에 대한 대시보드를 만들고 RBAC(역할 기반 액세스 제어)를 사용하여 해당 대시보드에 액세스할 수 있는 사용자를 제어할 수 있습니다. 따라서 데이터베이스 관리자에게는 SQL 데이터베이스 서비스 뷰가 있는 대시보드가 있고 Azure Active Directory 관리자에게는 Azure AD 내 사용자 및 그룹에 대한 뷰가 있을 수 있습니다.

대시보드는 .JSON(JavaScript Object Notation) 파일로 저장됩니다. 다른 컴퓨터에 업로드 및 다운로드되거나 Azure 디렉터리 멤버와 공유될 수 있음을 의미합니다. Azure는 포털 내에서 관리할 수 있는 가상 머신이나 저장소 계정과 같이 리소스 그룹 내에 대시보드를 저장합니다.

대시보드는 .JSON 파일이므로 대시보드를 프로그래밍 방식으로 사용자 지정하여 강력한 관리 도구를 만들 수도 있습니다. 또한 일부 타일 유형은 원본 데이터가 변경되면 자동으로 업데이트되도록 쿼리를 기반으로 할 수 있습니다.

## <a name="default-dashboard"></a>기본 대시보드

기본 대시보드는 간단히 대시보드로 이름이 지정되어 있습니다. 포털에 로그인하면 5개의 웹 파트가 포함된 이 대시보드가 표시됩니다.

![기본 웹 파트](../images/4-dashboard-default-webparts.png)

기본 웹 파트는 다음과 같습니다.

1. 모든 리소스
2. 빠른 시작 + 자습서
3. 서비스 상태
4. Marketplace
5. Azure 시작

## <a name="creating-and-managing-dashboards"></a>대시보드 만들기 및 관리

대시보드 맨 위에는 대시보드를 만들고, 업로드하고, 다운로드하고, 편집하고, 공유할 수 있는 컨트롤이 있습니다. 대시보드를 전체 화면으로 전환하거나 복제하거나 삭제할 수도 있습니다.

![대시보드 컨트롤 사용자 지정](../images/7-customise-dashboard-controls.PNG)

### <a name="select-dashboard"></a>대시보드 선택

왼쪽에는 대시보드 선택 드롭다운 컨트롤이 있습니다. 이 컨트롤을 클릭하면 계정에 대해 이미 정의한 대시보드 중에서 선택할 수 있습니다. 이 컨트롤을 사용하면 다양한 용도의 여러 대시보드를 간단히 정의한 후에 그때그때 수행하는 작업에 따라 수시로 한 대시보드에서 다른 대시보드로 쉽게 전환할 수 있습니다.

자신이 만드는 대시보드는 처음에는 비공개 상태입니다. 따라서, 자신만 해당 대시보드를 볼 수 있습니다. 대시보드를 엔터프라이즈 전체에서 사용할 수 있게 하려면 대시보드를 공유해야 합니다. 대시보드 공유/공유 해제에 대한 자세한 내용은 이후 섹션을 참조하세요.

### <a name="create-a-new-dashboard"></a>새 대시보드 만들기

새 대시보드를 만들려면 간단히 **새 대시보드**를 클릭합니다. 타일이 없는 대시보드 작업 영역이 표시됩니다. 이제 이 단원의 뒷 부분에 나오는 사용자 인터페이스를 통한 대시보드 편집 섹션에 자세히 설명된 대로 타일을 추가할 수 있습니다. 타일 추가 및 조정을 완료하고 대시보드 이름을 변경했으면 간단히 **사용자 지정 완료**를 클릭하여 저장하고 해당 대시보드로 전환합니다.

### <a name="upload-and-download"></a>업로드 및 다운로드

**업로드** 및 **다운로드** 단추를 사용하면 현재 대시보드를 .JSON 파일로 다운로드하고 사용자 지정하여 배포 및 업로드할 수도 있고, 다른 사용자가 해당 파일을 Azure Portal에 다시 업로드하여 해당 사용자의 현재 대시보드를 바꾸도록 할 수도 있습니다.

**다운로드**를 클릭하면 현재 대시보드가 기본 다운로드 폴더로 다운로드됩니다. 다운로드한 파일을 열면 .JSON 코드가 표시됩니다.

![대시보드 JSON 코드](../images/7-dashboard-json-code.PNG)

그러면 타일 크기 변경과 같이 수동으로 해당 코드를 편집하고 **업로드** 단추를 클릭하여 Azure에 다시 업로드할 수 있습니다.

### <a name="edit-a-dashboard"></a>대시보드 편집

이 항목에 대한 자세한 내용은 사용자 인터페이스를 통한 대시보드 편집 항목을 참조하세요.

### <a name="shareunshare-a-dashboard"></a>대시보드 공유/공유 해제

새 대시보드를 정의하면 해당 대시보드는 비공개 상태이며 자신의 계정에만 표시됩니다. 다른 사람에게 표시되도록 하려면 대시보드를 공유해야 합니다. 그러나 다른 모든 Azure 리소스와 마찬가지로 공유 대시보드를 저장할 리소스 그룹을 지정(또는 기존 리소스 그룹을 사용)해야 합니다. 기존 리소스 그룹이 없는 경우 Azure는 사용자가 지정하는 위치에 ‘대시보드’ 리소스 그룹을 만듭니다. 기존 리소스 그룹이 있는 경우 해당 리소스 그룹에 대시보드를 저장하도록 지정할 수 있습니다.

![공유 및 액세스 제어 1](../images/7-share-dashboards-default.PNG)

템플릿을 공유한 경우 두 번째 **공유 + 액세스 제어** 블레이드가 표시됩니다.

![공유 및 액세스 제어 2](../images/7-share-dashboards-access-control.PNG)

그러면 **사용자 관리**를 클릭하여 해당 대시보드에 액세스할 수 있는 사용자를 지정할 수 있습니다.

### <a name="switching-to-a-shared-dashboard"></a>공유 대시보드로 전환

공유 대시보드로 전환하려면 대시보드 목록을 클릭한 후에 **모든 대시보드 찾아보기**를 클릭합니다.

![모든 대시보드 찾아보기](../images/7-browse-dashboards.PNG)

이제 모든 공유 대시보드의 이름이 나와 있는 모든 대시보드 블레이드가 표시됩니다. 간단히 대시보드를 클릭하여 Azure Portal에 적용합니다.

![공유 대시보드](../images/7-select-shared-dashboard.png)

### <a name="display-a-dashboard-as-a-full-screen"></a>대시보드를 전체 화면으로 표시

대시보드를 최대 크기로 표시하려면 **전체 화면** 단추를 클릭하여 브라우저 메뉴 없이 현재 대시보드를 표시합니다. 화면 표시 경계를 벗어나는 타일이 있는 경우 화면 오른쪽과 아래쪽에 슬라이더 막대가 나타납니다.

전체 화면 모드에서 작업을 완료한 경우 Esc 키를 누르거나 화면 맨 위에 있는 대시보드 이름 옆의 **전체 화면 끝내기**를 클릭합니다.

### <a name="clone-a-dashboard"></a>대시보드 복제

대시보드를 복제하기만 하면 “(대시보드 이름) 복제본”이라는 인스턴트 복사본이 만들어지고 해당 복사본이 현재 대시보드로 전환됩니다. 복제를 사용하면 쉽게 대시보드를 만든 다음, 공유할 수 있습니다. 예를 들어 원하는 것과 거의 동일한 대시보드가 있는 경우 해당 대시보드를 복제하고 필요한 내용을 변경한 후에 공유하기만 하면 됩니다.

### <a name="delete-a-dashboard"></a>대시보드 삭제

대시보드를 삭제하면 사용 가능한 대시보드 목록에서 제거됩니다. 대시보드를 삭제할 것인지 확인하는 메시지가 표시되지만 삭제된 대시보드를 복구하는 기능은 없습니다.

## <a name="edit-a-dashboard-through-the-user-interface"></a>사용자 인터페이스를 통한 대시보드 편집

.JSON 파일을 다운로드하여 파일의 값을 변경하고 파일을 다시 Azure에 업로드하여 대시보드를 편집할 수는 있지만 이러한 방식은 사용자 인터페이스 설계에 사용하기가 매우 어렵습니다. GUI를 사용하여 현재 대시보드를 구성하려면 **편집** 단추를 클릭하거나 대시보드를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다. 대시보드가 편집 모드로 전환됩니다.

![대시보드 편집](../images/7-edit-dashboard.PNG)

왼쪽에 타일 갤러리가 표시되고 아래에 여러 타일이 보입니다. 타일 갤러리는 다음과 같은 기준으로 필터링할 수 있습니다.

* 일반
* type
* 검색
* 리소스 그룹
* 태그

![타일 갤러리](../images/7-tile-gallery.png)

이러한 각 옵션을 Azure Active Directory, 사물 인터넷, Microsoft Intune 등과 같은 범주별로 더 구체화할 수도 있습니다.

타일을 추가하려면 간단히 왼쪽 목록에서 타일을 선택하여 작업 영역으로 끌어서 놓기만 하면 됩니다. 그런 다음, 각 타일을 이동하거나 크기를 조정하거나 표시되는 데이터를 변경할 수 있습니다.

작업 영역이 편집 모드인 경우 사각형으로 나뉘어 있습니다. 타일마다 하나 이상의 사각형을 사용해야 하며 타일은 가장 가까운 최대 타일 구분선 집합에 맞춰집니다. 겹치는 타일은 방해되지 않도록 이동됩니다. 한 타일을 작게 만들면 주변 타일이 해당 타일에 맞춰 다시 위로 이동합니다.

### <a name="change-tile-sizes"></a>타일 크기 변경

일부 타일은 설정된 크기가 있으므로 프로그래밍 방식으로만 크기를 편집할 수 있습니다. 그러나 오른쪽 아래 회색 모서리가 있는 타일은 모서리 표시기를 끌어서 놓는 방법으로 편집할 수 있습니다.

![크기 조정 가능한 타일](../images/7-resizable-tile.png)

또는 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭하고 원하는 크기를 지정합니다.

![타일 크기](../images/7-tile-size.png)

대시보드를 만들려면 타일 갤러리에서 작업 영역으로 타일을 끌어온 후에 다시 정렬하기만 하면 됩니다.

### <a name="change-tile-settings"></a>타일 설정 변경

일부 타일에는 편집 가능한 설정이 있습니다. 예를 들어 시계 타일을 작업 영역으로 끌어오면 **시계 편집** 타일이 열립니다. 그러면 표시되는 표준 시간대를 설정하고 시간 표시도 12시간 형식인지 24시간 형식인지 설정할 수 있습니다.

![시계 편집](../images/7-edit-clock.png)

여러 국가 또는 여러 대륙에서 운영되는 기업의 경우 서로 다른 시간대의 시계를 더 추가할 수 있습니다.

### <a name="accepting-your-edits"></a>편집 수락

타일을 원하는 대로 정렬한 경우 **사용자 지정 완료**를 클릭하거나 마우스 오른쪽 단추를 클릭하고 **사용자 지정 완료**를 클릭합니다.

## <a name="edit-a-dashboard-by-changing-the-json-file"></a>.JSON 파일을 변경하여 대시보드 편집

.JSON 파일을 변경하여 대시보드를 편집할 수도 있습니다. 이 방법은 더 많은 설정 변경 옵션을 제공하지만 파일을 Azure로 다시 업로드할 때까지 변경 내용을 볼 수 없습니다.

![JSON 설정](../images/7-json-code.png)

위의 예에서 타일 크기를 변경하려면 colSpan 및 rowSpan 변수를 편집한 후 파일을 저장하고 Azure에 다시 해당 파일을 업로드합니다. 파일을 다른 사용자에게 배포할 수도 있습니다.

## <a name="reset-a-dashboard"></a>대시보드 다시 설정

모든 대시보드를 기본 스타일로 다시 설정할 수 있습니다. 편집 모드에서 마우스 오른쪽 단추를 클릭하고 **Reset to default state**(기본 상태로 다시 설정)를 선택합니다. 해당 대시보드를 다시 설정할 것인지 확인하는 대화 상자가 표시됩니다.

## <a name="summary"></a>요약

대시보드는 포털을 통해 Azure 서비스의 다양한 측면을 관리하는 데 사용되는 유연한 도구를 제공합니다. 대시보드를 통해 편리하게 서비스 상태를 모니터링할 수 있습니다. 대시보드는 공유할 수 있으므로 팀의 모든 구성원이 동일한 데이터를 보고 중요한 구성 요소의 상태를 계속 인식하고 있도록 하는 데 도움을 줍니다.