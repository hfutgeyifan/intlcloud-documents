## 소개

Cloud Object Storage(COS)의 일괄 작업 기능은 현재 다음을 포함하여 버킷의 객체에 대해 대규모 일괄 작업을 수행할 수 있습니다.

- 객체 복사
- 아카이브 객체 복구

처리할 객체를 객체 인벤토리 파일에 정리합니다. 해당 인벤토리 파일은 인벤토리 기능으로 생성된 인벤토리 보고서(먼저 [인벤토리 기능 활성화](https://intl.cloud.tencent.com/document/product/436/30624) 필요)이거나 사용자가 지정한 포맷에 따라 직접 생성할 수도 있습니다. COS 일괄 처리 기능은 해당 객체 인벤토리 파일에 따라 일괄 처리를 진행합니다. COS의 일괄 처리 작업 사용에 대한 자세한 정보는 [일괄 처리 개요](https://intl.cloud.tencent.com/document/product/436/32958)를 참고하십시오.

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **일괄 작업**을 클릭하여 일괄 작업 관리 페이지로 들어갑니다.
3. **작업 생성**을 클릭하여 일괄 처리 작업을 생성합니다.

다음은 설정 항목에 관한 설명입니다.
 - **작업 리전**: 작업을 생성할 리전을 선택합니다. 작업 리전은 사용자 인벤토리의 처리 대기 중인 객체의 버킷 기전과 동일해야 하며, 그렇지 않을 경우 실패합니다.
>? 현재 일괄 처리 기능은 중국대륙 공유 클라우드 리전에서만 지원되며 다른 리전에서는 지원되지 않습니다.
>
 - **인벤토리 포맷**: 인벤토리 객체에 사용할 유형을 선택하며, 다음과 같은 두 가지 포맷이 있습니다.
<table>
   <tr>
      <th>인벤토리 포맷</th>
      <th>필드</th>
      <th>설정 설명</th>
   </tr>
   <tr>
      <td nowrap="nowrap">COS 인벤토리 보고서</td>
      <td>-</td>
      <td>COS 생성 인벤토리 보고서 또는 사용자 정의 CSV 파일 선택</td>
   </tr>
   <tr>
      <td rowspan="3">CSV</td>
      <td>Bucket</td>
      <td>버킷 이름</td>
   </tr>
   <tr>
      <td>Key</td>
      <td>버킷에 있는 객체의 이름입니다. 객체 이름이 URL로 인코딩된 형식인 경우 사용하려면 먼저 일반 형식으로 디코딩해야 합니다.</td>
   </tr>
   <tr>
      <td>VersionId</td>
      <td>객체 버전 ID입니다. 버킷에 버전 제어를 활성화하면 COS는 버킷의 객체에 지정 버전을 추가합니다. 최신 버전이 아닌 객체 버전을 사용하고 싶은 경우 인벤토리에 포함된 객체의 버전 ID를 선택할 수 있습니다.</td>
   </tr>
</table>
 - **인벤토리 버킷**: 인벤토리가 있는 버킷을 선택합니다.
 - **인벤토리 파일 경로**: 인벤토리 파일 또는 CSV 파일의 경로를 각각 json 또는 csv 형식으로 지정합니다. 예를 들어 인벤토리 파일을 버킷 `examplebucket-1250000000`의 루트 디렉터리에 저장한 경우 인벤토리 경로는 `manifest.json`이 됩니다. 
4. **다음**을 클릭하고 작업 유형을 선택합니다.

다음은 설정 항목에 관한 설명입니다.
  - **데이터 일괄 복사**:
    - 타깃 버킷: 인벤토리 리스트에 있는 객체를 복사하여 붙여넣을 버킷입니다.
    - 접두사 작업: 복사한 객체에 접두사를 추가, 변경 및 삭제할 수 있습니다.
    - 스토리지 유형: 복사한 객체에 스토리지 유형을 설정합니다. 스탠다드 스토리지, 스탠다드IA 스토리지, 아카이브 스토지리, 딥 아카이브 스토리지를 선택할 수 있습니다.
    - 서버 암호화: 복사한 객체를 암호화할지 여부를 선택합니다. 암호화하지 않음, SSE-COS 암호화를 선택할 수 있습니다.
    - 액세스 권한: 복사한 객체에 액세스 권한을 설정합니다. 모든 권한 복사, 모든 권한 변경, 신규 권한 추가를 선택할 수 있습니다.
    - 객체 메타데이터: 복사한 객체에 메타데이터를 설정합니다. 모든 메타데이터 복사, 모든 메타데이터 변경, 신규 메타데이터 추가를 선택할 수 있습니다.
    - 객체 태그: 복사한 객체에 객체 태그를 설정합니다. 모든 태그 복사, 모든 태그 변경, 신규 태그 추가를 선택할 수 있습니다.
  - **아카이브 스토리지 일괄 복구**:
    - 복구 모드: 표준 모드와 일괄 모드를 선택할 수 있으며, 복구 모드에 대한 자세한 내용은 [보관된 객체 복구](https://intl.cloud.tencent.com/document/product/436/30961)를 참고하십시오.
    - 사본 유효 기간: 사본이 몇 일 후 자동 만료되어 삭제할지 설정하며, 설정 범위는 최소 1일 최대 365일입니다.
5. **다음**을 클릭하고 다음 옵션을 구성합니다.

 - **작업 설명(옵션)**: 해당 항목 작업에 대한 설명으로 작성하지 않아도 됩니다.
 - **작업 우선순위**: 우선순위가 높은 작업을 우선적으로 실행하며, 0을 제외한 자연수를 입력합니다. 숫자가 클수록 우선순위가 높아집니다.
 - **작업 보고서**: 작업 보고서 생성 여부를 선택합니다.
 - **CAM 역할**: CAM 역할을 생성하거나 기존의 CAM 역할을 선택하여 COS에 작업 권한을 부여합니다.
>! 일괄 처리 작업은 CAM 역할 생성 방식을 통해 COS에 일괄 처리 권한을 부여해야 하며, CAM 역할에 대한 자세한 사항은 [CAM 역할 개요](https://intl.cloud.tencent.com/document/product/598/19420)를 참고하십시오.
>
6. **다음**을 클릭하고 설정한 일괄 처리 작업 구성을 확인하고 선택합니다. **이 옵션을 선택하면 생성 후 작업이 바로 시작됩니다. 상기 구성 정보가 올바른지 확인하십시오**.
필요에 따라 정보를 수정하려면 **수정** 또는 **이전**을 클릭합니다.

7. 모든 것이 올바른지 확인한 후 **생성**/**생성 및 실행**을 클릭합니다.
그런 다음 작업 리스트에서 방금 생성한 작업을 찾습니다. 작업을 취소하려면 오른쪽에서 **작업 취소**를 클릭합니다.



