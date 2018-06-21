# IBM Cloud Private 설치

## IBM Cloud Private CE (Community Edition) 설치하기
전체 튜토리얼은 [Knowledge Center] (https://www.ibm.com/support/knowledgecenter/SSBS6K_2.1.0.3/installing/install_containers_CE.html) 를 참고하시기 바랍니다.
본 실습은 실습의 편의성을 위해 하나의 Node (Single Node)에 Kubernetes 클러스터를 한번에  


### Pre-requisite
- Node 간 SSH 통신하도록 설정
  - 본 실습은 Single Node를 
### Step 1: Boot Node 에만 Docker를 설치하기
Boot Node 는 Kubernetes 클러스터를 설치 / 업데이트하는 Node 입니다. Boot Node는 주로 Master Node와 함께 사용되기도 하지요. Boot Node 에만 Docker를 설치하면 나머지 노드에는 설치 스크립트를 통해 자동으로 Docker가 설치 됩니다.

### Step 2: 설치 환경 셋업하기
Boot Node 는 Kubernetes 클러스터를 설치 / 업데이트하는 Node 입니다. Boot Node는 주로 Master Node와 함께 사용되기도 하지요. Boot Node 에만 Docker를 설치하면 나머지 노드에는 설치 스크립트를 통해 자동으로 Docker가 설치 됩니다.셋업하기
