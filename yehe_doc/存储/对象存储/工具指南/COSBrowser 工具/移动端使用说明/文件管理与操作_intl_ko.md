<span id="CreateFolder"></span>
## 폴더 생성

COSBrowser 모바일 버전을 사용하면 다음과 같이 버킷에 폴더를 생성할 수 있습니다.

1. 버킷 리스트 또는 파일 리스트 페이지 우측 상단의 **+**를 클릭합니다.
2. 표시된 작업 리스트에서 **폴더 생성**을 클릭합니다.

3. 폴더 생성 페이지에서 폴더 이름을 입력하고 **확인**을 클릭합니다.


<span id="DeleteFolder"></span>
## 폴더 삭제

>! 폴더를 삭제하면 폴더 아래에 있는 모든 파일과 서브 디렉터리가 삭제됩니다.
>

#### 작업 순서

1. 대상 폴더 오른쪽의 **...**를 클릭합니다.
2. 표시된 작업 리스트에서 **삭제**를 클릭합니다.



<span id="UploadFile"></span>
## 파일 업로드

COSBrowser 모바일 버전을 사용하여 로컬 및 원격 파일 및 다른 App 또는 파일 관리자의 파일을 Cloud Object Storage(COS)로 업로드하고 업로드 중 파일 스토리지 유형, 액세스 권한, 암호화 방법, 객체 태그, 메타데이터 등의 정보를 설정할 수 있습니다. 다음 두 가지 방법으로 작업 리스트를 입력할 수 있습니다.

- 버킷 리스트 페이지 우측 상단의 **+**를 클릭합니다.

- 파일 리스트 페이지에서 오른쪽 상단의 **+**를 클릭합니다.



<span id="UploadPicturesAndVideos"></span>
### 이미지/동영상 업로드

COSBrowser를 사용하면 앨범에서 COS로 이미지 또는 비디오를 일괄 업로드할 수 있습니다.

#### 작업 순서

1. 작업 리스트에서 **이미지 업로드**를 클릭합니다.
2. 표시된 앨범의 파일 목록에서 대상 파일을 선택하고 **다음**을 클릭합니다.

3. (옵션) 업로드 매개변수를 구성합니다. COSBrowser를 사용하면 업로드하는 동안 다음 파일 속성을 설정할 수 있습니다.
 - **스토리지 유형**: 비즈니스 시나리오에 따라 객체의 스토리지 유형을 선택합니다. 기본적으로 스탠다드로 설정되어 있습니다. 자세한 내용은 [개요](https://intl.cloud.tencent.com/document/product/436/6222)를 참고하십시오.
  - **액세스 권한**: 필요에 따라 객체에 대한 액세스 권한을 선택합니다. 이 필드는 기본적으로 상속으로 설정됩니다(즉, 버킷의 권한 상속). 자세한 내용은 [액세스 제어 기본 개념](https://intl.cloud.tencent.com/document/product/436/30581)을 참고하십시오.
  - **서버 측 암호화**: 업로드하려는 객체에 대한 서버 측 암호화를 구성합니다. COS는 기록된 데이터를 자동으로 암호화하고 액세스할 때 암호를 해독합니다. 현재 COS는 SSE-KMS(베이징, 상하이, 광저우 리전에서만 사용 가능)와 SSE-COS의 두 가지 암호화 방법을 제공합니다. 자세한 내용은 [서버 암호화 개요](https://intl.cloud.tencent.com/document/product/436/18145)를 참고하십시오.
 - **객체 태그**: 객체 태그는 태그 키(tagKey), 태그 값(tagValue) 및 등호’=’로 구성됩니다(예: group = IT). 지정된 객체의 태그를 설정, 쿼리 및 삭제할 수 있습니다.
 - **메타데이터**: 객체 메타데이터는 또는 HTTP Header는 HTML 데이터를 브라우저로 보내기 전에 HTTP를 통해 서버에서 보내는 문자열입니다. HTTP Header를 수정하면 웹 페이지가 응답하는 방식과 캐싱 시간과 같은 특정 구성을 수정할 수 있습니다. 객체의 HTTP Header를 수정해도 객체 자체는 수정되지 않습니다. 자세한 내용은 [사용자 정의 Headers](https://intl.cloud.tencent.com/document/product/436/13361)를 참고하십시오.

4. **업로드**를 클릭하면 이미지와 동영상을 이미지 앨범에 일괄 업로드할 수 있습니다.


<span id="UploadFile;ink"></span>
### 링크를 통한 파일 업로드

COSBrowser를 사용하면 파일 링크를 통해 파일을 업로드할 수 있습니다. App에 들어갈 때마다 현재 클립보드를 확인합니다. 클립보드에 유효한 파일 링크가 있으면 링크를 통해 파일을 업로드할지 묻는 메시지가 나타납니다. 이 경우 **지금 업로드**를 클릭하기만 하면 됩니다.


다음과 같이 링크를 통해 파일을 업로드할 수도 있습니다.

1. 버킷 리스트 또는 파일 리스트 페이지에서 우측 상단의 **+**를 클릭하면 작업 리스트가 표시됩니다.
2. **링크 업로드**를 클릭하고 파일 업로드 링크를 텍스트 상자에 붙여넣고 업로드 경로를 선택하고 **업로드**를 클릭합니다.


<span id="UploadThirdPartySharing"></span>
### 3rd party 앱에서 공유한 파일 업로드 중

다른 App의 파일을 COSBrowser에 공유하여 업로드할 수도 있습니다.

>! 이 기능을 사용하려면 3rd party 앱이 다른 App과의 파일 공유를 지원해야 합니다.
>

#### 작업 순서

QQ를 예로 들어 보겠습니다.
1. QQ App에서 파일을 클릭하여 미리 보고 오른쪽 상단 모서리에 있는 **...**을 클릭한 다음 **기타 앱**을 선택합니다.

2. 앱 목록에서 COSBrowser를 클릭합니다.



<span id="UploadFileManager"></span>
### 파일 관리자에서 파일 업로드

COSBrowser는 시스템 파일 관리자(iOS에서는 파일, Android에서는 해당 시스템 파일 관리자 App)에서 COS로 파일을 업로드할 수 있습니다.

#### 작업 순서

1. 버킷 리스트 또는 파일 리스트 페이지에서 **+**를 클릭합니다.
2. 표시된 작업 리스트에서 **파일 업로드**를 클릭합니다.
3. 표시된 파일 관리자 페이지에서 대상 파일을 클릭합니다.



<span id="BackupFile"></span>
## 파일 백업

COSBrowser는 자동 백업 기능을 제공합니다. 이 기능이 활성화되면 COSBrowser는 앨범의 파일을 지정된 버킷에 자동으로 백업합니다. 백업 파일 관리를 돕기 위해 COSBrowser는 백업 데이터를 홈페이지에 별도의 모듈로 표시합니다.

>!
> - 앨범 백업 기능은 루트 계정에서만 지원됩니다.
> - 앨범 모듈은 이미지 및 비디오 파일만 표시합니다. 모든 파일을 보려면 버킷 리스트로 이동하여 백업 버킷을 검색하십시오.
>




<span id="SetBackup"></span>
### 백업 설정

**개인 > 앨범 백업**으로 이동하여 자동 사진 백업 또는 자동 비디오 백업을 활성화합니다.

- **자동 사진 백업**: 활성화되면 앨범의 모든 이미지가 백업됩니다.
- **자동 동영상 백업**: 활성화되면 앨범의 모든 동영상이 백업됩니다.
- **WIFI를 통해서만 백업**: 활성화되면 파일이 Wi-Fi 네트워크를 통해서만 백업됩니다.
- **리전**: 백업 리전을 선택하면 기본적으로 리전에 ‘from-phone-date-APPID’라는 버킷이 생성됩니다.
>! 리전은 백업이 활성화되기 전에만 설정할 수 있으며, 설정을 저장한 후에는 수정할 수 없습니다.
>
- **스마트 스토리지 활성화**: 활성화되면 앨범의 파일이 인텔리전트 티어링의 COS에 업로드됩니다. COS는 데이터 검색 비용이 발생하지 않고 인텔리전트 티어링 객체의 액세스 빈도를 기반으로 스탠다드 및 스탠다드_IA 유형 사이를 자동으로 전환하므로 스토리지 비용이 절감됩니다. 자세한 내용은 [인텔리전트 티어링 스토리지 소개](https://intl.cloud.tencent.com/document/product/436/38305)를 참고하십시오.


<span id="ManageBackupFiles"></span>
### 백업 파일 관리

COSBrowser는 파일 일괄 업로드 및 다운로드를 지원합니다.

#### 작업 순서

1. **앨범** 페이지에서 우측 상단의 일괄 작업 아이콘을 클릭하면 작업 버튼이 나타납니다.

2. 대상 파일을 선택하고 **다운로드** 또는 **삭제**를 클릭하여 파일을 다운로드하거나 삭제합니다.



<span id="AddFileToBackupBucket"></span>
### 백업 버킷에 파일 추가

다른 버킷의 이미지 또는 비디오 파일을 백업 버킷에 추가하여 **앨범** 모듈에서 빠르게 미리 볼 수도 있습니다.

#### 작업 순서

1. 대상 이미지 또는 동영상 파일의 오른쪽에 있는 **...**을 클릭합니다.
2. 표시된 작업 리스트에서 **앨범에 추가**를 클릭합니다.

3. **앨범** 모듈을 다시 입력하여 파일을 봅니다.

<span id="DownloadFile"></span>

## 파일 다운로드

COSBrowser를 사용하면 COS에서 로컬 파일 시스템으로 파일을 다운로드할 수 있습니다. 또한 시스템 앨범에 이미지를 저장할 수 있습니다.


<span id="DownloadToApp"></span>
### App에 다운로드 중

COSBrowser는 언제 어디서나 파일을 다운로드할 수 있도록 여러 다운로드 항목을 제공합니다.

- 방식1:
 1. 파일 리스트 페이지에서 대상 파일 오른쪽의 **...**를 클릭합니다.
 2. 표시된 작업 리스트에서 **다운로드 리스트에 추가**를 클릭합니다.
- 방식2:
파일 세부 정보 페이지에서 **...**를 클릭합니다. 표시된 작업 리스트에서 **다운로드**를 클릭합니다.
- 방식2:
파일 미리보기 페이지에서 오른쪽 상단의 **...**를 클릭합니다. 표시된 작업 리스트에서 **다운로드**를 클릭합니다.


<span id="SaveToGallery"></span>
### 앨범에 저장 중

COSBrowser를 사용하면 다음과 같이 로컬 앨범에 이미지를 저장할 수 있습니다.

1. 파일 리스트 페이지에서 대상 파일 오른쪽의 **...**를 클릭하여 작업 리스트를 표시합니다.
2. **다운로드**를 클릭하고 **앨범에 저장**을 선택합니다.


<span id="BatchOperation"></span>
## 일괄 작업

COSBrowser를 사용하면 버킷에서 파일을 일괄 다운로드, 삭제, 복사 및 이동할 수 있습니다.


<span id="BatchDownload"></span>
### 일괄 다운로드

1. 버킷을 클릭하여 파일 리스트 페이지로 이동한 후 오른쪽 상단의 **...**를 클릭합니다.
2. 표시된 작업 리스트에서 **일괄 작업**을 클릭합니다.

3. 파일을 일괄 선택하고 하단 작업 표시줄의 **다운로드**를 클릭합니다.
파일 리스트 페이지의 오른쪽 상단 모서리에 있는 전송 버튼을 클릭하여 전송 리스트 페이지에서 작업을 볼 수도 있습니다.


<span id="BatchDelete"></span>
### 일괄적으로 도메인 이름 삭제

1. 버킷을 클릭하여 파일 리스트 페이지로 이동한 후 오른쪽 상단의 **...**를 클릭합니다.
2. 표시된 작업 리스트에서 **일괄 작업**을 클릭합니다.

3. 일괄 선택 파일을 선택하고 하단 작업 표시줄에서 **더 보기 > 삭제**를 클릭합니다.


<span id="BatchCopy"></span>
### 일괄 복사

>? COSBrowser를 사용하여 소스 파일을 복사하면 ACL, Policy 및 Tagging과 같은 해당 정보도 복사됩니다.
>

1. 버킷을 클릭하여 파일 리스트 페이지로 이동한 후 오른쪽 상단의 **...**를 클릭합니다.
2. 표시된 작업 리스트에서 **일괄 작업**을 클릭합니다.

3. 파일을 일괄 선택하고 하단 작업 표시줄에서 **더 보기 > 복사**를 클릭합니다.



<span id="BatchMobile"></span>
### 일괄 이동

>? COSBrowser를 사용하여 소스 파일을 이동하면 ACL, Policy 및 Tagging과 같은 해당 정보도 이동됩니다.
>

1. 버킷을 클릭하여 파일 리스트 페이지로 이동한 후 오른쪽 상단의 **...**를 클릭합니다.
2. 표시된 작업 리스트에서 **일괄 작업**을 클릭합니다.

3. 파일을 일괄 선택하고 하단 작업 표시줄에서 **더 보기 > 이동**을 클릭합니다.



<span id="FilePreview"></span>
## 파일 미리보기

COSBrowser를 사용하면 이미지, 오디오, 비디오 및 문서와 같은 다양한 파일 형식을 미리 볼 수 있습니다. 또한 온라인 파일 압축 해제를 지원합니다.


<span id="ImagePreviewOnline"></span>
### 온라인 이미지 미리보기

COSBrowser를 사용하면 이미지를 다운로드하지 않고 온라인으로 미리 볼 수 있습니다.

#### 이미지 미리보기 활성화

다음 세 가지 방법으로 이미지를 미리 볼 수 있습니다.

1. 기능을 전역적으로 활성화

**개인 > 설정**을 선택하고 **이미지 미리보기**를 켭니다.


이 기능을 활성화한 후의 효과는 오른쪽과 같습니다.


2. 기능을 일시적으로 활성화

App을 처음 실행하고 파일 리스트 페이지에 들어가면 현재 리스트 페이지에 이미지가 포함되어 있는지 확인하고, 있다면 이미지 미리보기 활성화 여부를 묻는 팝업 창이 나타납니다. **미리보기 활성화**를 클릭하여 **이미지 미리보기** 기능을 빠르게 활성화할 수 있습니다. 이 기능이 필요하지 않은 경우 **취소**를 클릭할 수 있습니다. 나중에 사용하려면 **개인 > 설정**에서 수동으로 활성화할 수 있습니다.


3. 하나의 이미지에 대해 기능 활성화

**개인 > 설정**에서 이미지 미리보기를 비활성화하고 App을 처음 여는 것이 아닌 경우 이미지 세부 정보 페이지에 들어갈 때 앱에서 미리보기 활성화 여부를 묻습니다. 이 경우 **미리보기 클릭**을 클릭하여 파일을 미리 볼 수 있습니다.

>? 이 스위치는 전역 **이미지 미리보기** 토글의 상태를 변경하지 않습니다.
>



#### 큰 이미지 모드

COSBrowser는 이미지 세부 사항을 더 명확하게 볼 수 있도록 큰 이미지 모드 기능을 제공합니다.

1. 파일 리스트 페이지에서 대상 이미지를 클릭하여 파일 세부 정보 페이지로 이동합니다.
2. 이미지를 클릭하면 두 손가락으로 이미지를 확대하여 세부 정보를 볼 수 있는 큰 이미지 모드로 들어갑니다.
![](https://main.qcloudimg.com/raw/c5ded442635308a003ac6e98a740fdf6.jpg)


<span id="AudioDisplay"></span>
### 오디오 재생

COSBrowser는 mp3, ogg, aac, wma, wav, ape 또는 flag 형식의 오디오 파일을 재생할 수 있습니다.

#### 작업 순서

1. 파일 리스트 페이지에서 오디오 파일을 클릭하여 파일 세부 정보 페이지로 이동합니다.

2. 재생 버튼을 클릭합니다.
재생 속도를 높이거나 일시 중지할 수 있습니다.



<span id="VideoDisplay"></span>
### 비디오 재생

COSBrowser는 avi, wmv, mpeg, rm, rmvb, mkv, mov, qt 및 mp4와 같은 다양한 형식을 지원하는 간단한 온라인 비디오 재생 기능을 제공합니다. 시청 중에 비디오 재생 속도를 높이거나 일시 중지할 수 있습니다. App이 배경에 들어간 후 플로팅 창에서 비디오를 재생할 수도 있습니다.

#### 작업 순서

1. 파일 리스트 페이지에서 대상 동영상 파일을 클릭하여 파일 세부 정보 페이지로 이동합니다.
2. 재생 버튼을 클릭합니다.
재생 속도를 높이거나 일시 중지할 수 있습니다.

>? App이 백그라운드에 들어간 후에도 플로팅 창에서 비디오를 볼 수 있습니다.
>


<span id="DocumentPreview"></span>
### 문서 미리보기

COSBrowser를 사용하면 PDF와 같은 여러 형식의 파일을 미리 볼 수 있습니다.

#### 작업 순서

1. 대상 문서를 클릭하여 파일 세부 정보 페이지로 이동합니다. 문서 미리보기 기능을 활성화하지 않은 경우 **활성화 클릭**을 클릭합니다.

2. 문서 미리보기 기능 구성 페이지에서 **지금 활성화**를 클릭합니다.

3. 이전 페이지로 돌아가 **미리보기 클릭**을 클릭합니다.

4. 문서 미리보기 페이지에서 왼쪽으로 스와이프하여 다음 페이지를 봅니다.



<span id="UnzipFiles"></span>
## 파일 압축 해제

COSBrowser를 사용하면 온라인에서 zip, tar 또는 gz 형식의 파일 압축을 풀 수 있습니다. 압축 해제된 파일은 현재 디렉터리에 저장됩니다.

1. 파일 리스트 페이지에서 압축 파일 오른쪽의 **...**를 클릭합니다.

2. 표시된 작업 리스트에서 **온라인 압축 해제**를 클릭합니다.

3. 파일의 압축이 성공적으로 해제된 후 현재 디렉터리에 압축이 해제된 파일이 표시됩니다.



<span id="ShareFiles"></span>
## 파일 공유

COSBrowser는 데이터를 빠르게 수집하거나 버킷의 데이터를 다른 사용자와 공유할 수 있도록 폴더 및 파일 공유 기능을 제공합니다.


<span id="SharedFolder"></span>
### 공유 폴더

>?
> - 한 번에 하나의 폴더만 공유할 수 있고 여러 파일은 공유할 수 없습니다.
> - 루트 계정과 서브 계정의 공유 기간은 각각 최대 2시간 최대 1.5일까지 설정할 수 있습니다.
> - 여러 사용자가 폴더를 공유하는 경우 파일 내용을 관리하기 어려울 수 있습니다. 이 경우 버킷에 대한 버전 관리를 활성화하여 원하는 기록 버전으로 되감는 것이 좋습니다.
>

#### 공유 QR 코드/링크 생성

구체적인 작업 순서는 다음과 같습니다.

1. 폴더 오른쪽의 **...**를 클릭하고 표시된 작업 리스트에서 공유를 클릭합니다.

2. 표시된 공유 페이지에서 공유할 QR 코드 또는 링크를 선택할 수 있습니다.

3. (옵션) 아래와 같이 공유 매개변수를 구성합니다. 매개변수를 기본값으로 유지하려면 이 단계를 건너뛸 수 있습니다.

 - **권한**: 공유할 폴더에 대한 액세스 권한을 설정할 수 있습니다.
    - 읽기 전용: 액세스 URL을 통해 파일 리스트를 가져와 폴더에 있는 파일을 다운로드합니다.
    - 읽기/쓰기: 액세스 URL을 통해 파일 목록을 가져오고, 폴더에 파일을 다운로드하고, 폴더에 파일을 업로드하고, 폴더를 생성합니다.
 - **유효 기간**: 분, 시간 또는 일 단위입니다. 루트 계정과 서브 계정의 유효 기간은 기본적으로 각각 2시간과 24시간이며 변경할 수 없습니다.
 - **비밀번호**: 6자리 숫자, 문자, 특수기호를 포함할 수 있습니다. 기본적으로 시스템에서 자동으로 생성되지만 사용자 정의할 수 있습니다.
4. **링크 생성** 또는 **QR 코드 공유**를 클릭하여 공유 링크 또는 QR 코드를 생성합니다.



### 다른 사용자가 공유한 폴더 보기

모바일 또는 PC 클라이언트에서 다른 사용자가 공유한 폴더를 열 수 있습니다.

**방법1: 모바일에서 보기**

1. **로그인** 또는 **개인** 페이지에서 **스캔**을 클릭하여 QR 코드를 스캔합니다.

2. 암호를 입력하고 **확인**을 클릭하여 공유 폴더를 봅니다.


**방법2: PC에서 보기**

1. 로그인 페이지에서 **공유 링크로 로그인**을 클릭합니다.

2. 획득한 URL 주소와 비밀번호를 입력하고 로그인합니다.


**방법3: 브라우저에서 보기**

1. 브라우저를 열고 공유 URL을 입력하여 엽니다.

2. 암호를 입력하고 **Extract**를 클릭하여 공유 폴더로 들어갑니다.


<span id="ShareFile"></span>
### 파일 공유

COS에 저장된 각 파일은 특정 URL을 통해 액세스할 수 있습니다. 버킷에 대해 다른 도메인 이름(예: CDN 가속 도메인 이름 및 사용자 지정 원본 도메인 이름)을 설정한 경우 지정된 도메인 이름으로 파일 URL을 생성할 수 있습니다. 파일이 비공개 읽기인 경우 특정 유효 기간이 있는 임시 액세스 URL을 생성하기 위해 임시 서명을 요청할 수 있습니다.

>!
>- 임시 키로 로그인할 경우 파일 URL의 유효 기간을 설정할 수 없으며 기본적으로 1시간입니다.
>- 파일이 공개 읽기인 경우 URL은 서명을 포함하지 않으며 영구적으로 유효합니다. 파일이 비공개 읽기인 경우 URL은 임시 서명을 포함하며 1시간 동안 유효합니다.
>

#### 작업 순서

1. 파일을 클릭하여 파일 세부 정보 페이지로 이동합니다.
다음은 설정 항목에 관한 설명입니다.
 - 도메인 지정: URL의 도메인 이름을 설정합니다(옵션).
 - 유효 기간: URL의 유효 기간을 설정합니다(옵션).
2. 구성이 올바른지 확인한 후 링크 생성을 클릭합니다.

3. 생성된 파일 URL을 전송합니다.



<span id="RenameFile"></span>
## 파일 이름 변경

>? 폴더 이름은 변경할 수 없습니다.
>

#### 작업 순서

1. 파일 오른쪽의 **...**를 클릭합니다.
2. 파일 작업 리스트에서 **이름 변경**을 클릭합니다.

2. 팝업 창에서 새 파일 이름을 입력하고 **확인**을 클릭합니다.
**중복 파일 덮어쓰기**를 선택하면 원본 파일을 덮어씁니다. 그렇지 않으면 새 파일이 생성됩니다. **개인 > 설정 > 기본 업로드 옵션 > 중복 파일 이름 바꾸기**에서 전역 덮어쓰기를 활성화할 수도 있습니다.



<span id="SearchFile"></span>
## 파일 검색

COSBrowser 모바일 버전은 퍼지 검색 및 유형별 검색 기능을 제공합니다. 접두사를 사용하여 현재 폴더와 서브 폴더에서 해당 파일 이름 접두사를 가진 파일을 검색할 수 있습니다. 파일 유형을 먼저 지정하여 해당 유형의 파일을 검색할 수도 있습니다.


<span id="SearchKeyword"></span>
### 키워드로 검색

검색 키워드를 입력하여 현재 폴더와 모든 서브 폴더에 있는 키워드를 포함하는 모든 파일 이름을 필터링할 수 있습니다.



<span id="SearchTypes"></span>
### 유형별 검색

COSBrowser를 사용하면 비디오, 폴더, 오디오, 문서, 이미지 등 유형별로 파일을 검색할 수 있습니다.

#### 작업 순서
폴더 검색을 예로 들면:

1. 검색 상자를 클릭한 다음 폴더를 클릭합니다.

2. 현재 디렉터리의 폴더 유형에 있는 모든 파일(여기서는 폴더)이 나열됩니다.



<span id="SortOrFilterObjects"></span>
## 객체 정렬 또는 필터링

COSBrowser를 사용하면 버킷의 파일을 정렬하고 필터링할 수 있습니다.
>? 현재 파일명/파일 크기/수정 시간별 정렬, 스토리지 유형별 필터링이 지원됩니다.
>

#### 작업 순서

1. 파일 리스트 페이지로 이동하여 검색창 오른쪽에 있는 필터 및 정렬 버튼을 클릭합니다.

2. 작업 리스트에서 버킷의 파일을 정렬하거나 필터링합니다.



<span id="ManageFilePermissions"></span>
## 파일 권한 관리

COSBrowser를 사용하면 버킷보다 우선 순위가 높은 파일에 대한 액세스 권한을 설정할 수 있습니다.

>!
> - 객체 액세스 권한은 기본 엔드포인트를 통해 액세스하는 경우에만 적용됩니다. CDN 가속 도메인 이름 또는 사용자 지정 엔드포인트를 통해 이루어진 모든 액세스에는 버킷 액세스 권한이 적용됩니다.
> - ACL 수에는 제한이 있습니다. 자세한 내용은 [규격 및 제한](https://intl.cloud.tencent.com/document/product/436/14518)을 참고하십시오.
>


<span id="ModifyPublicPermissions"></span>
### 공개 권한 수정

1. 대상 파일을 클릭하여 파일 세부 정보 페이지로 이동합니다.
2. 상단의 **권한 정보**를 클릭하여 권한 리스트 페이지로 이동합니다.

3. 공개 권한을 클릭하여 파일의 접근 권한을 수정합니다.<br>


<span id="SetUserPermissions"></span>
### 사용자 권한 설정

1. 대상 파일을 클릭하여 파일 세부 정보 페이지로 이동합니다.
2. 상단의 **권한 정보**를 클릭하여 권한 리스트 페이지로 이동합니다.

3. 공개 권한을 클릭하여 파일의 사용자 권한을 수정합니다.
**사용자 추가**를 클릭하여 사용자 권한을 추가할 수 있습니다. 사용자 권한을 왼쪽으로 스와이프하여 편집하거나 삭제할 수도 있습니다.



