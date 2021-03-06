손님이 많은 미장원에 일반적으로 고객이 약속을 지키지 않는 반복되는 문제가 있는 시나리오를 가정해 봅니다. 약속은 예약된 시간 슬롯입니다. 고객이 약속을 지키지 않으면 미장원은 손해를 봅니다. 이 문제를 수정하기 위해 미장원은 소프트웨어 개발자에게 연락합니다. 문제를 개선하기 위해 미리 알림 문자 메시지를 보내기로 합니다. 매일 아침에 그날 약속이 있는 모든 고객에게 문자 메시지를 보냅니다.

Azure 개발자는 Azure 함수를 사용하여 이 문제를 해결하기로 합니다. 문자 메시지를 보내는 논리를 구현하는 방법을 이미 알고 있습니다. 이제 특정 시간에 메시지를 보내는 방법을 알아봐야 합니다. 다행히 Azure Functions는 _트리거_라는 기능을 지원합니다. 트리거는 Azure 함수를 실행하는 방법을 결정하는 데 사용됩니다.

## <a name="learning-objectives"></a>학습 목표
> [!div class="checklist"]
> * 비즈니스 요구 사항에 가장 적합한 트리거를 결정합니다.
> * 일정한 일정에 따라 함수를 호출하는 타이머 트리거를 만듭니다.
> * HTTP 요청을 수신할 때 함수를 호출하는 HTTP 트리거를 만듭니다.
> * Azure Storage에서 Blob을 만들거나 업데이트할 때 함수를 호출하는 Blob 트리거를 만듭니다.
