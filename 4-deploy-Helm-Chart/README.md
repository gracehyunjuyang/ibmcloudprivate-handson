## Blue Compute 마이크로서비스를 Helm Chart로 배포하기

Helm Chart를 카탈로그에 추가하는 방법은 크게 두가지입니다. 

- Helm Chart가 저장되어 있는 repository 추가하기 
  - [Kubernetes stable chart](https://github.com/kubernetes/charts/tree/master/stable)와 [Kubernetes incubator chart](https://github.com/kubernetes/charts/tree/master/incubator) 등 Open source 활용   
  - repository 직접 구성하여 추가
  
- Helm Chart를 직접 작성하여 추가
  - Helm CLI를 통해 직접 Chart를 패키징하여 카탈로그에 추가
  
 이번 시간에는 시간 제약상 Helm Chart의 모든 것을 다루지는 못하고,
 
 맛보기로 정도로 
 Helm repository를 추가하고
 카탈로그에 추가된 Chart를 배포하는 간단한 실습을 해보겠습니다. 
 
 이번에 배포해 볼 Helm Chart는 여러개의 마이크로서비스로 이루어져 있는 Bluecompute 앱입니다. 
 Bluecompute 마이크로서비스 아키텍처입니다. 
 
 ![Alt Bluecompute architecture](./images/bluecompute-0.png)

### 1. Helm Chart repository 추가하기 

1. **메뉴 > Manage > Helm Repositories** 클릭
2. 이미 등록된 레파지토리 목록이 있습니다. 참고로 `local-charts`는 IBM Cloud Private 내에 위치한 로컬 레파지토리 입니다. 
3. 우측 상단 `Add repository` 클릭 
 ![Alt Bluecompute](./images/bluecompute-2.png)
 
4. 추가할 레파지토리 정보 입력
  - Name : ibmcase
  - URL : https://raw.githubusercontent.com/ibm-cloud-architecture/refarch-cloudnative-kubernetes/master/docs/charts/bluecompute-ce
  
  ![Alt Bluecompute](./images/bluecompute-3.png)
  
5. **Sync Repository** 카탈로그 동기화
  ![Alt Bluecompute](./images/bluecompute-4.png)
  
6. 동기화 후 우측 상단 버튼을 클릭해 **카탈로그**로 이동
  ![Alt Bluecompute](./images/bluecompute-5.png)

7. 이제 **bluecompute-ce** 라는 서비스가 추가되었습니다. 


### 2. 카탈로그에서 Helm Chart 배포하기

1. **bluecompute-ce** 차트를 클릭
  ![Alt Bluecompute](./images/bluecompute-6.png)

2. bluecompute 차트를 배포할 때 숙지해야 하는 내용과 옵션들을 명시해 놓은 `README.md` 내용입니다. **Configure** 클릭
  ![Alt Bluecompute](./images/bluecompute-7.png)
  
3. 필요한 옵션을 입력
- Release name : bluecompute-ce
- Target namespace : default

그 외 내용은 수정하지 않고 그대로 진행하겠습니다. 

필요시 별도 스토리지를 사용하려면 PersistentVolumeClaim을 명시하면 됩니다. 
그러나 본 튜토리얼에서는 편의를 위해 hostpath를 사용하도록 하겠습니다.

다양한 옵션 값으로부터 볼 수 있듯이 
Auth, Catalog, Catalogelasticsearch 등 여러개의 서비스가 Bluecompute 애플리케이션을 이루는 하나의 패키지로 배포될 것입니다. 

  ![Alt Bluecompute](./images/bluecompute-8.png)

4. **Install** 을 클릭해 Chart를 배포
  ![Alt Bluecompute](./images/bluecompute-9.png)

5. 배포 후 **View Helm Release**를 클릭해 배포 현황 확인 
  ![Alt Bluecompute](./images/bluecompute-10.png)
  
6. Helm Release 정보 확인 
  ![Alt Bluecompute](./images/bluecompute-11.png)

약 3-4분 후 모든 pod의 상태가 **AVAILABLE** = 1 이 되면 모든 서비스가 모두 UP 된 것입니다. 

7. 우측 상단 **LAUNCH** 버튼을 클릭해 배포된 서비스를 확인 
  ![Alt Bluecompute](./images/bluecompute-12.png)
  ![Alt Bluecompute](./images/bluecompute-13.png)

Bluecompute 애플리케이션을 여기저기 투어해보세요. 
각 페이지별로 서로 다른 마이크로서비스가 호출됩니다. 

  



