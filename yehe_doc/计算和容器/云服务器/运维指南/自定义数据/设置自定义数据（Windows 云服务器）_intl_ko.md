## 작업 시나리오

CVM을 생성할 때 **사용자 정의 데이터**를 지정하여 인스턴스를 구성할 수 있습니다. CVM을 **처음 시작**할 경우 사용자 정의 데이터는 텍스트 모드로 CVM에 전달된 뒤 텍스트가 실행됩니다. 한 번에 여러 CVM을 구매할 경우 사용자 정의 데이터는 모든 CVM이 처음 시작할 때 해당 텍스트를 실행합니다.

본 문서에서는 Windows CVM을 처음 시작할 경우 PowerShell 형식을 통해 전달하는 스크립트 예시입니다.

## 주의 사항

- 사용자 정의 데이터를 지원하는 Windows 운영 체제는 다음과 같습니다.
 - Windows Server 2019 데이터센터 에디션 64비트 영어 에디션
 - Windows Server 2016 데이터센터 에디션 64비트 영어 에디션
 - Windows Server 2012 R2 데이터센터 에디션 64비트 영어 에디션
- CVM을 처음 시작할 경우에만 텍스트 전달을 통해 명령어를 실행하십시오.
- Base64 인코딩 전 사용자 정의 데이터는 16KB를 초과할 수 없습니다.
- 사용자 정의 데이터는 Base64 인코딩을 통해 전달되므로 base64가 아닌 스크립트 파일을 복사할 경우 ‘base64 양식 텍스트로 입력’을 선택하지 마십시오.
- 시작할 때 사용자 정의 데이터에서 지정된 작업을 실행하면 서버 시작에 소요되는 시간이 증가합니다. 작업이 완료된 후, 작업이 성공적으로 실행되는지 테스트하길 권장합니다.
- 본 예시에서 PowerShell 태그를 사용하여 Windows PowerShell 스크립트를 지정하십시오. 예를 들면 <powershell></powershell> 태그입니다.

## 작업 단계

### 텍스트 준비

사용자의 실제 요구에 따라 텍스트를 준비하십시오.


#### PowerShell 스크립트[](id:PowerShellScript)
PowerShell 태그를 사용하여 PowerShell 스크립트 텍스트를 준비합니다.
예를 들어 사용자가 CVM의 C: 디스크에 ‘Hello Tencent Cloud.’인 ‘tencentcloud.txt’ 파일을 생성해야 할 경우 PowerShell 태그를 사용하여 다음과 같은 내용을 준비할 수 있습니다.
```shell
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```


#### Base64 인코딩 스크립트[](id:Base64Script)

1. 아래의 명령어를 실행하여 ‘script_text.psl’이라는 PowerShell 스크립트 파일을 생성하십시오.
```shell
vi script_text.ps1
```
2. **i**를 눌러 편집 모드로 바꾸고, 다음의 내용을 참고하여 ‘script_text.ps1’을 입력한 뒤 스크립트 파일을 저장합니다.
```shell
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```
3. 아래의 명령어를 실행하여 ‘script_text.psl’ 스크립트 파일에 Base64 인코딩 작업을 진행하십시오.
```shell
base64 script_text.ps1
```
다음의 정보를 출력합니다.
```shell
PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAgQzpcdGVuY2VudGNsb3VkLnR4dAo8L3Bvd2Vyc2hlbGw+Cg==
```

### 텍스트 전달

Tencent Cloud는 인스턴스를 시작하는 다양한 방법을 제공하며, 주로 다음 두 가지 경우로 나뉩니다. 사용자의 실제 필요에 따라 선택하십시오.

<dx-tabs>
::: 공식 웹 사이트 또는 콘솔을 통해 전달[](id:Consoletrans)

1. [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하여 인스턴스를 구매하고 ‘2. 호스트 설정’에서 **고급 설정**을 클릭하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/283fb3e0e1400d4ba5725c8b6a1ea279.png)
2. ‘고급 설정’에서 실제 요구에 따라 ‘사용자 정의 데이터’의 텍스트 박스에 준비한 내용을 입력하십시오.
 - PowerShell 스크립트: [PowerShell 스크립트](#PowerShellScript)를 입력합니다.
 - Base64 인코딩 스크립트: 먼저 ‘base64 양식 텍스트로 입력’을 선택하고 다시 [Base64 인코딩 스크립트](#Base64Script)를 아래 이미지와 같이 입력합니다.
 ![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
3. 인터페이스의 작업 절차에 따라 CVM 생성을 완료합니다.
:::
::: API를 통해 전달[](id:APItrans)
API를 통해 CVM을 생성할 경우 [Base64 인코딩 스트립트](#Base64Script)에 리턴된 인코딩 결과를 RunInstances 인터페이스의 UserData 파라미터에 할당하여 텍스트를 전달합니다.
예를 들어 UserData 파라미터로 CVM에 대한 요청 파라미터를 생성하는 예는 다음과 같습니다.
```shell
https://cvm.tencentcloudapi.com/?Action=RunInstances
&Version=2017-03-12
&Placement.Zone=ap-guangzhou-2
&ImageId=img-pmqg1cw7
&UserData=PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAuXHRlbmNlbnRjbG91ZC50go=
&<공통 요청 매개변수>
```
:::
</dx-tabs>



### 사용자 정의 데이터 구성 검증

1. CVM에 로그인합니다.
2. 운영 체제 인터페이스에서 C:\ 디스크를 열고 `tencentcloud.txt` 텍스트 파일이 있는지 조회합니다.
`tencentcloud.txt` 텍스트 파일이 있을 경우 아래 이미지와 같이 성공적으로 구성된 것입니다.
![](https://main.qcloudimg.com/raw/9f94ec922111734a489b9730d66168c3.png)


### 실행 로그 보기
스크립트 실행 로그에 대한 `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\log\cloudbase-init.log` 파일을 볼 수 있습니다.

