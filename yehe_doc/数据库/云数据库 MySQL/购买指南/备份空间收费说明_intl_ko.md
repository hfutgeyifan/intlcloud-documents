## 개요
백업 공간은 자동 데이터 백업, 수동 데이터 백업 및 로그 백업을 포함하여 한 리전의 모든 TencentDB for MySQL 인스턴스의 백업 파일을 저장하는 데 사용됩니다.

TencentDB for MySQL은 리전에 따라 일정 한도의 백업 용량을 무료로 제공합니다. 무료 백업 용량의 크기는 해당 리전에 있는 2노드와 3노드 인스턴스(프라이머리 인스턴스, 재해 복구 인스턴스 포함)의 스토리지 용량 합계입니다. 해당 리전의 계산 예시는 [계산식](#jfgs)을 참고하십시오.
>?
>- 읽기 전용 인스턴스 RO를 구매 시 백업 공간을 증정하지 않습니다. 프라이머리 인스턴스와 장애 복구 인스턴스를 구매 시에만 증정합니다. 
>- 백업 공간 크기는 [MySQL 콘솔](https://console.cloud.tencent.com/mysql/backup/index)의 데이터베이스 백업 페이지에서 확인할 수 있습니다. 

## 백업 가격
백업 용량이 무료 할당액을 초과할 경우, 중국대륙 리전은 0.000113USD/GB/시간을 기준으로 요금이 부과됩니다. 기타 리전의 가격은 [TencentDB for MySQL 가격 계산기](https://buy.intl.cloud.tencent.com/price/cdb/calculator)를 참고하십시오.
요금 과금 대상 공간이 1GB 미만일 경우, 실제 요금이 차감되지 않습니다. 1시간 미만은 1시간으로 집계합니다. TencentDB for MySQL은 유연한 증정 정책을 적용하므로 대부분의 인스턴스는 백업 공간에 따른 요금이 부과되지 않습니다.

## 리전 간 백업 및 과금 관련 설명[](id:kdybfjjfsm)
TencentDB for MySQL는 규정 준수 또는 재해 복구를 위한 리전 간 백업을 지원합니다. [리전 간 백업](https://www.tencentcloud.com/document/product/236/50652)의 지침에 따라 콘솔에서 이 기능을 활성화할 수 있습니다. 활성화되면 리전 간 백업은 로컬 기본 백업에 영향을 미치지 않으며 보존 기간을 개별적으로 설정할 수 있습니다. 자동 백업이 완료되면 리전 간 백업을 위해 저장 장치에 덤프됩니다.

>!리전 간 백업 및 로그 파일은 여유 저장 공간을 사용하지 않으며 원본 인스턴스 백업 리전의 저장 공간을 사용합니다.

리전 간 백업 공간의 가격은 중국 대륙 기준 0.000113 USD/GB/시간, 중국 대륙 외부 기준 0.000127 USD/GB/시간으로 책정됩니다.
리전 간 백업 기능은 현재 베이징, 상하이, 광저우, 선전 및 청두에서 사용할 수 있으며 앞으로 더 많은 리전에서 제공될 예정입니다.

## 백업 요금 부과 시간
- 2019년 12월 02일 0시부터 홍콩·마카오·타이완 지역(중국 홍콩)과 기타 중국 외 리전에서 요금을 부과합니다.
- 2019년 12월 02일 00:00부터 중국 남서부(청두 및 충칭 리전), 화남, 화동, 화북에 대한 정식 과금이 시작되었습니다.
- 2019년 12월 05일 0시부터 화남지역(광저우)에서 요금을 부과합니다.
- 2019년 12월 09일 0시부터 화북지역(베이징)에서 요금을 부과합니다.
- 2019년 12월 10일 0시부터 화동지역(상하이)에서 요금을 부과합니다.
- 2019년 12월 10일 0시 이후에 추가된 리전에 대해 백업 요금이 정식 과금됩니다.


## [계산 공식](id:jfgs)
**무료 백업 공간(단일 리전) = 해당 리전에서 구매한 MySQL 2노드 및 3노드 인스턴스의 스토리지 공간 합계**

**유료 사항(단일 리전)= 데이터 백업량(해당 리전)+ 로그 백업량(해당 리전)- 무료 백업 공간(해당 리전)**

>?휴지통의 TencentDB for MySQL 인스턴스 백업도 백업 공간에 포함됩니다.

**계산 예시**
예를 들면 광저우 3존에서 실행 중인 MySQL 2노드 인스턴스(구매한 데이터베이스 스토리지 공간: 월 500GB)와 광저우 4존에서 실행 중인 MySQL 2노드 인스턴스(구매한 데이터베이스 스토리지 공간: 월 200GB)가 있을 경우, 광저우 리전은 매월 700GB 공간을 무료로 사용할 수 있습니다.

광저우 리전의 총 백업 공간이 700GB를 초과할 경우, 초과분은 별도로 과금됩니다. 예를 들어, 데이터 백업이 800GB에 이르고 로그 백업이 100GB에 달하면, 해당 시간당 과금 공간은 200GB(800 + 100 - 700 = 200GB)이며, 초과분 과금은 이런 방식으로 계속 이어집니다.


## 백업 라이프사이클
### 정액 과금제 인스턴스
- 백업은 인스턴스의 라이프사이클 기반으로 변화합니다
- 백업 기능은 인스턴스가 만료된 후 7일 이내에 정상적으로 사용할 수 있으며, 이 기간 동안에는 프리 티어를 초과하는 백업 공간에 대해서는 요금이 계속 청구됩니다.
- 만료 후 8일째부터 인스턴스는 휴지통으로 격리됩니다. 이 때 자동 백업이 중지되고 롤백 및 수동 백업이 금지되지만 백업은 계속 다운로드할 수 있습니다 ([백업 리스트](https://console.cloud.tencent.com/mysql/backup/list/data) 페이지에서 다운로드 가능). 인스턴스의 백업 공간은 인스턴스가 완전 삭제될 때까지 계속 청구됩니다. 콘솔의 휴지통에 있는 인스턴스를 갱신하여 복구할 수 있습니다.
- 인스턴스가 휴지통에서 격리된 후 7일이 지나면 모든 데이터 백업과 함께 인스턴스가 제거(즉, 완전히 삭제)됩니다. 필요한 백업을 저장하십시오.

### [종량제 인스턴스](id:anliang_zhouqi)
- 백업은 인스턴스의 라이프사이클 기반으로 변화합니다
- 인스턴스 연체 24시간 이내, 정상적으로 백업합니다.
- 24시간 후 인스턴스는 휴지통으로 격리됩니다. 이 때 자동 백업이 중지되고 롤백 및 수동 백업이 금지됩니다. 그러나 백업은 계속 다운로드할 수 있습니다 ([백업 리스트](https://console.cloud.tencent.com/mysql/backup/list/data) 페이지에서 다운로드 가능). 인스턴스의 백업 공간은 인스턴스가 완전 삭제될 때까지 계속 청구됩니다. 콘솔의 휴지통에 있는 인스턴스를 갱신하여 복구할 수 있습니다.
- 휴지통에서 3일 경과 후 모든 데이터 백업과 함께 인스턴스가 비활성화되고 종료됩니다. 필요한 백업을 적시에 저장하시기 바랍니다.

## 계정 연체 설명
### 정액 과금제 인스턴스
- 인스턴스가 만료되지 않았지만 계정에 연체된 결제가 있는 경우 백업 서비스가 다운그레이드되고 롤백, 수동 백업 및 백업 다운로드가 금지되지만 자동 백업은 계속되어 과도한 백업 공간이 계속 청구됩니다.
- 롤백, 수동 백업 또는 백업 다운로드를 수행해야 하는 경우 계정에 잔액을 충전하십시오.

### 종량제 인스턴스
계정이 연체되면, 백업은 사용자의 인스턴스 라이프사이클 기준으로 변화됩니다. 상기 종량제 백업 라이프사이클 관련 소개를 참고하십시오.

## 백업 과금 시작 후 업그레이드된 서비스 이용 가능
>?아래 표에 각각 나열된 값은 단일 Tencent Cloud 계정이 같은 리전에서 지원하는 최대값입니다.

| 업그레이드 내용             | 업그레이드 전         | 업그레이드 후          |
| ------------------ | -------------- | --------------- |
| 데이터 백업 유지 기간   | 30일             | 1830일             |
| 로그 백업 유지 기간 | 5일              | 1830일             |
| 백업 압축률         | 일반 압축률              | 고압축률               |
| binlog 중앙화         | 로컬 스토리지 | 중앙화 스토리지 |

## 백업 비용 절감을 위한 제안
- 사용하지 않는 수동 백업 데이터를 삭제합니다. 수동 백업은 [MySQL 콘솔](https://console.cloud.tencent.com/cdb) 인스턴스 관리 페이지(해당 인스턴스 ID 또는 **작업** 열에서 **관리**를 클릭하여 입력)> 백업 복구 페이지에서 삭제 가능합니다. 자동 백업은 만료 후 자동 삭제되며, 콘솔에서 수동 삭제가 불가능합니다.
- 비핵심 작업 데이터의 자동 백업 빈도를 낮춥니다. 콘솔에서 백업 주기 및 백업 보관 기간을 변경할 수 있으며, 백업은 1주에 최소 2회 이상 진행합니다.
>?[데이터베이스 롤백](https://intl.cloud.tencent.com/document/product/236/7276)은 백업 주기와 백업 보관일 내의 데이터 백업+로그 백업(binlog)을 기반으로 합니다. 자동 백업의 빈도수와 보관일 단축은 인스턴스 데이터의 롤백 시간 범위에 영향을 미치므로, 백업 설정의 밸런스를 적절히 조절하시기 바랍니다.
>
- 비핵심 비즈니스의 데이터 백업 및 로그 백업 보관 기간을 줄입니다. 백업 유지 기간은 7일이며 대부분 시나리오의 요구사항을 충족합니다.

| 비즈니스 시나리오             | 백업 유지 기간                                                 |
| -------------------- | ------------------------------------------------------------ |
| 핵심 서비스             | 7일 - 1830일 권장                                              |
| 비핵심, 비데이터류 비즈니스 | 7일 권장                                                      |
| 아카이브 비즈니스             | 데이터 백업 유지 기간은 7일을 권장합니다. 실제 비즈니스 니즈에 따라 수동으로 데이터를 백업하고 사용 완료 즉시 삭제합니다. |
| 테스트 비즈니스             | 데이터 백업 유지 기간은 7일을 권장합니다. 실제 비즈니스 니즈에 따라 수동으로 데이터를 백업하고 사용 완료 즉시 삭제합니다. |

