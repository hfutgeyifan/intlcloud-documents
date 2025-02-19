[IM 콘솔](https://console.cloud.tencent.com/im)에 로그인하여 대상 애플리케이션 카드를 클릭하고 왼쪽 사이드바에서 **그룹 관리**를 선택하여 비즈니스 니즈에 따라 그룹을 관리할 수 있습니다.
REST API 호출을 통해 그룹을 관리할 수도 있습니다. 자세한 내용은 [App의 모든 그룹 가져오기](https://intl.cloud.tencent.com/document/product/1047/34960)를 참고하십시오.


## 그룹 추가
1. **그룹 관리** 페이지에서 **그룹 추가**를 클릭합니다.
2. 그룹 추가 팝업 창에서 다음 매개변수를 설정합니다.
 - 그룹 이름: 필수 입력 사항으로 길이는 30바이트를 초과하지 않아야 합니다.
 - 그룹 소유자 ID : 선택 입력 사항으로, 이미 등록된 사용자 이름을 입력해야 합니다.
 - 그룹 유형 : 업무 그룹, 공개 그룹, 미팅 그룹, 라이브 방송 그룹 등 그룹 유형을 설정합니다. 그룹 관련 자세한 안내는 [그룹 시스템](https://intl.cloud.tencent.com/document/product/1047/33529)을 참고하십시오.
3. **확인**을 클릭하여 설정을 저장합니다.
 그룹 생성 후, 그룹 목록에서 그룹 ID, 그룹 이름, 그룹 소유자, 유형, 생성 시간을 확인할 수 있습니다.

## 그룹 세부 정보 보기
**그룹 관리** 페이지에서 대상 그룹이 있는 행의 **상세 보기**를 클릭하여 **그룹 세부 정보** 페이지로 이동하여 그룹의 기본 정보 조회 및 수정, 그룹 구성원을 관리를 진행할 수 있습니다.

### 기본 정보 수정
1. **그룹 세부 정보**페이지에서 기본 정보 섹션의 **편집**을 클릭합니다.
2. 그룹 정보 수정 팝업 창에서 그룹 이름과 그룹 소개를 수정할 수 있습니다.
 ![](https://main.qcloudimg.com/raw/e02ca8b347201a324fe8c6816024a725.png)
3. **확인**을 클릭하여 설정을 저장합니다.

### 그룹 구성원 관리
**그룹 구성원 추가**
1. **그룹 세부 정보**페이지에서 그룹 구성원 관리 섹션의 **그룹 구성원 추가**를 클릭합니다.
2. 구성원 추가 팝업 창에서 사용자 이름을 입력합니다.
 >? 등록된 사용자 이름을 입력해야 합니다.
 >
![](https://main.qcloudimg.com/raw/a770c24a1c91813e16e50da0616f22ba.png)
3. **확인**을 클릭하여 설정을 저장합니다.
 그룹 구성원 추가 완료 후, 그룹 구성원 목록에서 사용자 이름, 닉네임, 참여 시간, 마지막 발언 시간 및 구성원 역할을 볼 수 있습니다.

**그룹 구성원 삭제**
1. **그룹 세부 정보**페이지에서 다음 방법으로 그룹 구성원을 삭제할 수 있습니다.
 - 개별 삭제: 대상 그룹 구성원이 있는 행의**삭제**를 클릭합니다.
 - 일괄 삭제: 삭제할 대상 그룹 구성원을 모두 체크하고, 그룹 구성원 목록 상단의 **그룹 구성원 삭제**를 클릭합니다.
2. 팝업창에서 **확인**을 클릭합니다.
 삭제 후 선택한 구성원은 더 이상 그룹에 속하지 않습니다.

## 메시지 발송
1. **그룹 관리** 페이지에서 다음과 같은 방법으로 메시지를 보낼 수 있습니다.
 - 그룹 메시지 개별 발송: 대상 그룹이 있는 행의 **메시지 발송**을 클릭합니다.
 - 그룹 메시지 일괄 발송: 메시지를 보낼 모든 대상 그룹을 선택하고 그룹 목록 상단의 **메시지 발송**을 클릭합니다.
2. 그룹 메시지 발송 팝업 창에서 메시지 내용을 입력합니다.
 >?메시지 길이는 300자 이하이어야 합니다.
 >
3. **확인**을 클릭하여 메시지를 보냅니다.

## 그룹 해산
**해산 후에는 모든 그룹 정보가 삭제되며 복원할 수 없습니다. 주의하시기 바랍니다. **

1. **그룹 관리** 페이지에서 다음과 같은 방법으로 그룹을 해산할 수 있습니다.
 - 개별 해산: 대상 그룹이 있는 행의 **해산**을 클릭합니다.
 - 일괄 해산: 해산할 대상 그룹을 모두 체크하고, 그룹 목록 상단의 **그룹 해산**을 클릭합니다.
2. 해산 확인 팝업 창에서 **확인**을 클릭합니다.
 **해산 후에는 모든 그룹 정보가 삭제되며 복원할 수 없습니다. **

