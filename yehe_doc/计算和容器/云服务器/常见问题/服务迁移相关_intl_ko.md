## 오프라인 마이그레이션

### COS 업로드 및 마이그레이션에는 왜 이렇게 많은 시간이 소요되나요?
업로드 소요 시간은 이미지 파일 크기, 대역폭 크기 등에 따라 달라집니다. 압축된 이미지 포맷(qcow2 또는 vhd)을 사용하여 전송 시간과 마이그레이션 시간을 단축할 수 있습니다.

### 마이그레이션 작업에 실패한 이유가 무엇인가요?
 - 현재 Tencent Cloud의 서비스 마이그레이션은 qcow2, vhd, vmdk 및 raw 이미지 포맷을 지원합니다. 이미지가 이 포맷에 해당하는지 확인하시기 바랍니다.
 - 이미지 파일의 COS 업로드 여부와 COS 권한을 확인하여 임시 링크 유효성과 파일 손상 여부를 확인하십시오.
 - 마이그레이션 시 대상 CVM/CBS의 사용 상태가 정상이어야 합니다. 만료 상태의 디바이스에서는 마이그레이션을 완료할 수 없습니다.

### 마이그레이션 작업 시 나타나는 오류는 어떻게 해결해야 하나요? 
- **‘이미지 파일 메타데이터 획득 실패’** 메시지가 나타난 경우, 손상된 이미지 파일 또는 지원하지 않는 이미지 파일 포맷이 일반적인 원인입니다. 이미지 생성/내보내기, 이미지 업로드 등의 단계에서 오류가 발생하진 않았는지, 이미지 파일 포맷이 qcow2, vhd, vmdk 또는 raw인지 확인한 후 다시 시도하시기 바랍니다.
- **‘이미지 압축 해제 실패’** 메시지가 표시되면 일반적으로 이미지 생성 오류입니다. 이미지 압축 패키지의 정확성을 확인하거나 이미지를 다시 내보내고 타깃 디스크의 용량이 다음과 같은지 확인하십시오. 원본 디스크보다 큰 경우 다시 시도하십시오.
- **‘타깃 장치의 스토리지 공간이 너무 작음’** 메시지가 나타난 경우, 현재 마이그레이션 작업의 타깃 시스템 디스크 또는 데이터 디스크의 저장 용량이 원본 디스크에 비해 작거나 이미지 파일보다 작은 것이 일반적인 원인입니다. 타깃 시스템 디스크 또는 데이터 디스크의 용량을 조정하여 타깃 디스크의 용량이 그보다 큰지 확인하십시오. 원본 디스크를 선택한 다음 다시 시도하십시오.
- **‘cos 이미지 파일 액세스 실패’** 메시지가 표시되면 일반적으로 COS 권한 문제이므로 COS 파일이 있는 리전이 현재 리전과 동일한지 확인하고 COS 권한을 확인하십시오. 임시 링크의 유효성을 확인하고 다시 시도하십시오.
- **‘타깃 디스크로 이동 실패’** 메시지가 표시되면 가능한 원인은 일반적으로 다음과 같습니다.
 - 타깃 디스크의 용량이 너무 작습니다.
 - 이미지 생성 중 오류가 발생했습니다.
 하나씩 진단하고 다시 시도하십시오.
- **‘작업 시간 초과’**, **‘시스템 오류’**, **‘기타 원인’** 등의 메시지가 나타나거나 마이그레이션 작업을 다시 시도했는데도 여전히 실패하는 경우 [고객센터](https://intl.cloud.tencent.com/document/product/213/34837)를 통해 문제를 해결할 수 있습니다.


## 온라인 마이그레이션의 일반적인 문제

### 온라인 마이그레이션은 어떤 운영 체제와 디스크 유형을 지원하나요?
- Linux의 주요 운영 체제(예시: Centos 또는 Ubuntu 등)를 모두 지원합니다.
- 디스크 유형 및 용량과는 무관합니다.


### 온라인 마이그레이션과 이미지 가져오기에는 어떤 차이가 있나요?
온라인 마이그레이션은 이미지 가져오기와 유사하며, 원본 시스템을 Tencent Cloud로 옮길 수 있습니다. 가장 큰 차이는 온라인 마이그레이션은 수동 이미지 생성 또는 이미지 내보내기/가져오기를 하지 않고도 클라우드 업로드가 가능하다는 점입니다. 원본 기기에서 직접 시스템과 데이터를 클라우드에 전송하기만 하면 됩니다.


### 온라인 마이그레이션은 원본 공용 IP를 마이그레이션하나요?
마이그레이션하지 않습니다. 온라인 마이그레이션은 원본 시스템 및 데이터만 동기화하며, 공용 IP는 마이그레이션할 수 없습니다.


### 마이그레이션 툴은 중단 지점부터 이어서 전송을 지원하나요?
지원합니다. 데이터 전송 단계에서 중단된 경우 다시 툴을 실행하면 전송이 복구됩니다.


### 마이그레이션을 완료한 후에도 툴을 보관해야 하나요?
보관하지 않아도 됩니다. 마이그레이션 완료 후, 원본 서버에서 직접 삭제할 수 있습니다.


### 마이그레이션 속도와 요금은 어떻게 되나요?
- 속도: 주로 대상 CVM의 대역폭에 종속되며, 테스트는 1코어 1G 메모리, 사용량 과금 대역폭은 12Mbps인 CVM을 사용하며 실제 마이그레이션 속도는 약 9Mbps입니다. 구체적인 계산 방법은 [마이그레이션 시간 예상 튜토리얼](https://intl.cloud.tencent.com/document/product/213/44342)을 참고하십시오.
- 요금: 마이그레이션 툴 자체는 무료입니다. 마이그레이션 과정에서 대역폭 등 리소스로 인해 소량의 요금이 발생하게 되며, 요금은 트래픽 및 시간 과금 규정에 따라 산정됩니다. 자세한 내용은 공식 홈페이지에서 가격을 확인하십시오.


### 여러 CVM의 동시 마이그레이션을 지원하나요?
지원합니다. 여러 서버의 마이그레이션을 동시에 진행할 수 있습니다. 각각 다른 대상 CVM으로 마이그레이션하기 때문에 서로 영향을 주지 않습니다.


### Virtio를 어떻게 확인하고 설치하나요?
Virtio 확인 및 설치 작업에 대한 자세한 내용은 [Linux 시스템 Virtio 드라이버 확인](https://intl.cloud.tencent.com/document/product/213/9929)을 참고하십시오.


### Rsync는 어떻게 설치하나요? [](id:installRsync)
원본 서버의 운영 체제에 따라 해당 명령을 선택하여 Rsync를 설치합니다.
- CentOS：`yum -y install rsync`
- Ubuntu、Debian：`apt-get -y install rsync`
- SUSE：`zypper install rsync`
 다른 Linux 릴리스 버전의 경우 해당 릴리스 버전의 공식 웹사이트에서 설치 문서를 참고하십시오.


### SELinux를 비활성화하는 방법은 무엇입니까? [](id:closeSELinux)
`/etc/selinux/config` 파일을 편집하고 `SELINUX=disabled`를 설정합니다.


## 콘솔 온라인 마이그레이션 관련 문제

### 툴은 어디서 다운받나요?
[여기](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)를 클릭하여 콘솔 온라인 마이그레이션 툴 압축 패키지를 다운로드할 수 있습니다. [콘솔 온라인 마이그레이션 사용 가이드](https://intl.cloud.tencent.com/document/product/213/44338)를 참고하여 작업하십시오.


### 마이그레이션 원본을 가져오는 방법은 무엇입니까?
1. [콘솔 온라인 마이그레이션 툴](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)을 다운로드하고 압축 해제합니다.
2. 원본 호스트의 해당 아키텍처에 대한 실행 파일을 실행하여 마이그레이션 원본을 온라인 마이그레이션 콘솔로 가져옵니다.
 - 32비트 원본 호스트는 `go2tencentcloud_x32`를 실행합니다.
 - 64비트 원본 호스트는 `go2tencentcloud_x64`를 실행합니다.


### 마이그레이션 원본을 업데이트하거나 마이그레이션 원본을 다시 가져오는 방법은 무엇입니까?
마이그레이션 원본 디스크 등 기타 정보가 변경된 경우 마이그레이션 원본 정보를 업데이트하거나 마이그레이션 원본을 다시 가져와야 합니다. 그런 다음 마이그레이션 원본을 먼저 삭제한 다음 클라이언트를 다시 실행하여 마이그레이션 원본을 가져오십시오.


### 마이그레이션 원본은 어떻게 삭제하나요?
[온라인 마이그레이션 콘솔](https://console.cloud.tencent.com/cvm/csm/online?rid=1)에 로그인하여 마이그레이션 원본이 있는 행 오른쪽의 **삭제**를 클릭한 후 확인을 클릭하면 삭제됩니다. 마이그레이션 원본에 완료되지 않은 마이그레이션 작업이 연결되어 있는 경우 마이그레이션 작업을 일시 중지하고 삭제한 후 마이그레이션 원본을 삭제하십시오.


### 마이그레이션 전에 대상 CVM 인스턴스를 선택하는 방법은 무엇입니까?
대상 CVM의 운영 체제는 원본 호스트의 운영 체제와 동일한 것이 좋습니다. 예를 들어 CentOS 7 시스템을 원본 호스트로 마이그레이션할 때 CentOS 7 시스템 CVM을 마이그레이션 대상으로 선택합니다.


### 마이그레이션 작업은 어떤 상태일 때 완료되었다고 표시됩니까?
마이그레이션 작업의 상태가 ‘성공’인 경우에만 완료 상태를 나타내며 나머지는 미완료 상태입니다.


### 마이그레이션 작업을 삭제하는 방법은 무엇입니까?
마이그레이션 작업의 실제 상태에 따라 다음 작업을 수행하십시오.
- 마이그레이션 작업이 ‘시작되지 않음’ 또는 ‘성공’인 경우 마이그레이션 작업이 있는 행 오른쪽의 **삭제**를 클릭하여 마이그레이션 작업을 직접 삭제할 수 있습니다.
- 마이그레이션 작업 ‘실패’ 시 마이그레이션 작업을 삭제해야 하는 경우 마이그레이션 원본을 온라인 상태로 유지해야 합니다. 마이그레이션 작업이 있는 행 오른쪽의 **삭제**를 클릭하여 마이그레이션 작업을 삭제합니다. 이 경우 작업은 ‘삭제 중’이 되며 마이그레이션 툴은 마이그레이션 작업에서 생성된 리소스를 자동으로 정리하고 마이그레이션 작업을 삭제합니다.


### 마이그레이션이 너무 오래 걸리고 마이그레이션을 취소하고 싶다면 어떻게 해야 하나요?
이 경우 [온라인 마이그레이션 콘솔](https://console.cloud.tencent.com/cvm/csm/online?rid=1)에 로그인하여 마이그레이션 작업을 일시 중지하고, 일시 중지 후 마이그레이션 작업이 있는 행 오른쪽의 **삭제**를 클릭하여 마이그레이션 작업을 삭제하고 마이그레이션 작업을 취소할 수 있습니다.


### 만약 전송 인스턴스가 폐기되면 어떻게 합니까?
대상 Tencent Cloud 이미지로 마이그레이션할 때 생성된 전송 인스턴스가 실수로 폐기된 경우 현재 마이그레이션 작업을 삭제하고 마이그레이션 원본에 대해 새 작업을 생성하여 마이그레이션 작업을 실행할 수 있습니다.


### 콘솔을 사용하여 마이그레이션 오류가 발생하거나 실패하면 어떻게 해야 합니까?
마이그레이션 시 오류가 발생하거나 실패하는 원인은 매우 다양하며, 일반적으로 다음의 몇 가지가 있습니다.


- 대상 CVM으로 마이그레이션 시 대상 CVM의 보안 그룹이 80, 443 포트가 개방되지 않은 경우.
**해결 방법**: 대상 CVM의 보안 그룹 규칙을 수정하여 포트 80 및 443을 개방합니다.
- 대상 CVM으로 마이그레이션 시 대상 CVM의 디스크 용량이 부족한 경우.
**해결 방법**: 서버에 용량이 충분한 디스크를 마운트하고 용량이 충분한 CVM을 다시 선택한 다음 마이그레이션 작업을 다시 생성하여 마이그레이션을 시작합니다.
- 대상 Tencent Cloud 이미지로 마이그레이션한 후 전송 인스턴스 생성 시 오류가 보고됩니다. 예: ‘Failed create transit instance, maybe no available source in target region’.
**해결 방법**: 마이그레이션 작업의 대상 리전에 사용 가능한 리소스가 없을 수 있으며, 이 경우 마이그레이션할 다른 리전을 선택하거나 지정된 CVM으로 마이그레이션을 사용하여 문제를 해결할 수 있습니다.

여전히 문제를 해결할 수 없거나 위의 예시에 속하지 않는 경우, 현재 마이그레이션 로그 파일(기본적으로 마이그레이션 툴 디렉터리의 log 파일)을 보관하고 [고객센터](https://intl.cloud.tencent.com/document/product/213/34837)를 통해 해결하십시오.



### 마이그레이션이 완료되면 무엇을 받게 됩니까?
마이그레이션 작업이 완료된 후 플랫폼은 마이그레이션 작업에서 설정한 대상 유형에 따라 해당 마이그레이션 제품을 생성합니다.
- 대상 유형 **CVM 이미지** 선택: 마이그레이션이 완료되면 마이그레이션 원본에 대한 대상 Tencent Cloud 이미지가 생성되며, 마이그레이션 작업이 있는 행의 **CVM 이미지 ID**를 클릭하면 [CVM 이미지 페이지](https://console.cloud.tencent.com/cvm/image/index)에서 이미지 세부 정보를 조회할 수 있으며 이미지를 사용하여 CVM을 빠르게 생성할 수 있습니다. CVM 이미지가 성공적으로 생성되면 해당 이미지와 연결된 **CVM 스냅샷**이 동기식으로 생성됩니다.
- 대상 유형으로 **CVM 인스턴스** 선택: 마이그레이션이 완료된 후 마이그레이션 원본이 대상 Tencent Cloud CVM 인스턴스로 마이그레이션됩니다.


### Linux 서버 마이그레이션 후 시스템 확인은 어떻게 하나요?
대상 CVM이 정상적으로 실행되는지, 대상 CVM의 데이터가 소스 CVM과 일치하는지, 네트워크가 정상적인지 또는 다른 시스템 서비스가 정상적인지 등을 확인하시기 바랍니다.


### 마이그레이션이 완료된 후 다시 마이그레이션해야 하는 경우 어떻게 해야 하나요?
[온라인 마이그레이션 콘솔](https://console.cloud.tencent.com/cvm/csm/online?rid=1)에 로그인하여 마이그레이션 원본을 사용하여 마이그레이션 작업을 다시 생성하고 실행합니다.


## 온라인 마이그레이션 툴 관련 문제


### 툴은 어디서 다운받나요?
[여기](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)를 클릭하여 마이그레이션 툴 압축 패키지를 다운로드할 수 있습니다. [툴 마이그레이션 작업 사용 가이드](https://intl.cloud.tencent.com/document/product/213/35640)를 참고하여 작업하십시오.


### 툴은 어떻게 사용하나요?
마이그레이션 툴을 원본 서버에 다운로드하거나 업로드하여 기기의 실제 상황에 따라 구성 파일을 수정한 다음 마이그레이션 툴을 실행해야 합니다. 마이그레이션을 일괄 수행해야 하는 경우 스크립트를 작성하여 일괄 처리할 수 있습니다.


### 툴을 사용하여 마이그레이션할 때 오류나 실패가 보고되면 어떻게 해야 합니까?

마이그레이션 시 오류가 발생하거나 실패하는 원인은 매우 다양하며, 일반적으로 다음의 몇 가지가 있습니다.
- 대상 CVM 보안 그룹에 80, 443포트가 개방되지 않은 경우.
- 원본에서 마이그레이션 시 데이터 디스크가 있으나, user.json의 DataDisks 필드에 원본 데이터 디스크 마이그레이션 설정을 하지 않아 모든 데이터를 대상 CVM 시스템 디스크로 발송할 때 디스크 용량 부족 현상이 발생하는 경우.
- [내부 네트워크 마이그레이션 시나리오](https://intl.cloud.tencent.com/zh/document/product/213/44340#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F)에서 3단계 마이그레이션을 수행하지 않아 대상 CVM이 마이그레이션 모드를 종료한 경우.

여전히 문제를 해결할 수 없거나 위의 예시에 속하지 않는 경우, 현재 마이그레이션 로그 파일(기본적으로 마이그레이션 툴 디렉터리의 log 파일)을 보관하고 [고객센터](https://intl.cloud.tencent.com/document/product/213/34837)를 통해 해결하십시오.



  

