일반적으로 논리는 설정 간격으로 실행됩니다. 블로그 소유자이며 구독자가 가장 최근 게시물을 읽지 못하는 것을 알았다고 가정합니다. 구독자에게 블로그를 확인하도록 미리 알리기 위해 매주 한 번 메일을 보내는 것이 가장 적합하다고 결정합니다. 타이머 트리거와 함께 Azure 함수를 사용하여 이 논리를 구현하고 매주 함수를 호출합니다.

여기서는 타이머 트리거를 만들고 일정 간격으로 실행되도록 트리거에 지시하는 방법을 알아봅니다.

## <a name="what-is-a-timer-trigger"></a>타이머 트리거란?

타이머 트리거는 일정 간격으로 함수를 실행하는 트리거입니다. 타이머 트리거를 만들려면 두 가지 정보를 제공해야 합니다. 첫 번째 요구 사항은 ‘타임스탬프 매개 변수 이름’으로, 코드의 트리거에 액세스하기 위한 식별자입니다. 두 번째 요구 사항은 ‘일정’으로, 타이머의 간격을 설정하는 ‘CRON 식’입니다.

## <a name="what-is-a-cron-expression"></a>CRON 식이란?

‘CRON 식’은 시간 집합을 나타내는 6개의 필드로 구성된 문자열입니다.

Azure에서 6개 필드의 순서는 {second} {minute} {hour} {day} {month} {day of the week}입니다.

예를 들어 5분마다 실행되는 트리거를 만드는 ‘CRON 식’은 다음과 같습니다.

```
0 */5 * * * *
```

처음에는 이 문자열이 혼동될 수 있습니다. 돌아와서 ‘CRON 식’을 더 자세히 살펴볼 때 이러한 개념을 분류해 보겠습니다.

‘CRON 식’을 빌드하려면 일부 특수 문자를 기본적으로 이해해야 합니다.

| 특수 문자 | 의미 | 예 |
| ------------- | ------------- | ------------- |
| *      | 필드에서 모든 값 선택 | 요일 필드의 별표 “*”는 ‘매’일을 의미합니다. |
| .      | 목록에서 항목 구분 | 요일 필드의 쉼표 “1,3”은 월요일(1일) 및 수요일(3일)을 의미합니다. |
| -      | 범위 지정 | 시간 필드의 하이픈 “10-12”는 시간 10, 11 및 12를 포함하는 범위를 의미합니다. |
| /      | 증분 지정 | 분 필드의 슬래시 “*/10”은 10분마다 발생하는 증분을 의미합니다. |

이제 원래 CRON 식 예제로 돌아갑니다. 필드별로 필드를 분류하여 더 잘 살펴보겠습니다.

```
0 */5 * * * *
```

**첫 번째 필드**는 초를 나타냅니다. 이 필드는 0-59 값을 지원합니다. 필드에 0이 포함되어 있으므로 첫 번째 가능한 값(1초)을 선택합니다.

**두 번째 필드**는 분을 나타냅니다. “*/5” 값에는 두 개의 특수 문자가 포함됩니다. 먼저 별표(*)는 “필드에서 모든 값 선택”을 의미합니다. 이 필드는 분을 나타내므로 가능한 값은 0-59입니다. 두 번째 특수 문자는 증분을 나타내는 슬래시(/)입니다. 이들 문자를 결합하면 모든 값 0-59에서 매 5번째 값을 선택합니다. 간단하게 말하면 “5분마다”입니다.

**나머지 4개 필드**는 시간, 날짜, 월 및 요일을 나타냅니다. 이러한 필드의 별표는 모든 가능한 값을 선택함을 의미합니다. 이 예제에서는 “매월 매일 매시간”을 선택합니다.

모든 필드를 함께 넣으면 식은 “매월 매일 매시간 5분마다 첫 번째 1초”를 의미합니다.

## <a name="how-to-create-a-timer-trigger"></a>타이머 트리거를 만드는 방법

타이머 트리거는 완전히 Azure Portal에서 만들 수 있습니다. Azure 함수의 미리 정의된 트리거 형식 목록에서 **타이머 트리거**를 선택합니다. 실행할 논리를 입력합니다. **타임스탬프 매개 변수 이름** 및 **CRON 식**을 제공합니다.

## <a name="summary"></a>요약

타이머 트리거는 지정된 일정으로 Azure 함수를 호출합니다. 타이머 트리거의 일정을 정의하려면 시간 집합을 나타내는 문자열인 ‘CRON 식’을 빌드합니다.

