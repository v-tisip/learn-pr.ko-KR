교통 카메라에 사용되는 데이터를 처리하는 회사에서 일한다고 가정해 보겠습니다. 비디오 스트림을 분석, 분류, 처리하여 특정 시간의 사람 얼굴과 차량 번호판을 식별합니다. 그런 다음, 이 정보를 Azure Data Lake에 업로드하면 검색 가능한 인덱스가 생성됩니다.

이러한 비디오 스트림에서는 다양한 코덱과 해상도를 사용합니다. 여러 Windows 기반 전용 소프트웨어 패키지를 실행하여 초기 처리를 수행하고 공통 비디오 형식으로 인코딩해야 합니다. 정기적으로 새로운 형식이 릴리스되므로 VM(가상 머신)에서 비디오 처리를 수행하는 것이 좋습니다. 그러면 전체 시스템을 중지하지 않고 전용 패키지를 추가 및 업데이트할 수 있습니다.

Windows Virtual Machines의 인코딩 소프트웨어를 관리하려면 사용자 인터페이스에 연결해야 합니다.

이 모듈에서는 Windows 가상 머신을 만들고 RDP(원격 데스크톱 프로토콜)를 사용하여 연결하는 방법을 배웁니다.

## <a name="learning-objectives"></a>학습 목표
> [!div class="checklist"]
> * Azure Portal을 사용하여 Windows 가상 머신을 만듭니다.
> * Azure의 가상 머신에 사용할 수 있는 옵션을 이해합니다.
> * Windows 원격 데스크톱 연결을 사용하여 실행 중인 Windows 가상 머신에 연결합니다.

## <a name="prerequisites"></a>필수 조건

- Azure Cloud Services 환경에 대한 지식이 있어야 합니다.
- 가상 머신에 익숙해야 합니다.
