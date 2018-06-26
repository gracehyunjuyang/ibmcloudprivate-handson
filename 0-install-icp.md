# IBM Cloud Private 설치 
본 매뉴얼에서는 IBM Cloud Private을 ICP로 줄여서 칭하겠습니다.

## IBM Cloud Private CE (Community Edition) 설치하기
설치 매뉴얼 전문은 [Knowledge Center](https://www.ibm.com/support/knowledgecenter/SSBS6K_2.1.0.3/installing/install_containers_CE.html) 를 참고하시기 바랍니다.
본 실습은 편의성을 위해 Single Node에 Kubernetes 클러스터를 한번에 설치합니다.

실습 시간 단축을 위해 Step 1 까지는 모두 구성 완료하였습니다. 
Step 2부터 시작하시면 됩니다. Step 2 입니다!! :-)

### Pre-requisite (구성 완료. SKIP)
- Node 간 SSH 통신하도록 설정 
- `/etc/hosts` 파일에 hostname 입력
- 그 외 포트 설정 등 ICP 설치를 위한 환경 구성


### Step 1: Boot Node 에 Docker를 설치하기 (구성 완료. SKIP)
Boot Node 는 Kubernetes 클러스터를 설치, 업데이트하는 노드로 주로 Master Node와 함께 설치 됩니다. 
Boot Node 에 Docker를 설치하면 나머지 노드에는 ICP 설치 과정에서 자동으로 Docker가 설치 되므로, Boot Node 에만 Docker를 설치합니다. 


### Step 2: 설치 환경 셋업하기
1. Boot Node에 root 권한으로 로그인
2. [Docker Hub](https://hub.docker.com/r/ibmcom/icp-inception/)로부터 IBM Cloud Private-CE 설치 이미지 다운로드.
```
 sudo docker pull ibmcom/icp-inception:2.1.0.3
```

3. ICP 설정 파일을 저장하기 위한 설치 디렉토리 생성
 ```
 mkdir /opt/ibm-cloud-private-ce-2.1.0.3;  \
 cd /opt/ibm-cloud-private-ce-2.1.0.3
 ```
 
 4. 설정 파일 압축 풀기
 ```
 sudo docker run -e LICENSE=accept \
 -v "$(pwd)":/data ibmcom/icp-inception:2.1.0.3 cp -r cluster /data
 ```
`cluster` 디렉토리는  설치 디렉토리 안에 생성됨. `/opt` 밑에 `/opt/cluster` 와 같이 생성됨

 5. 클러스터를 구성하는 노드간 secure connection 을 생성하기 위해 SSH Key 생성 
 ``` 
 ssh-keygen -b 4096 -f ~/.ssh/id_rsa -N ""
 ```
 6. 생성된 key를 authorized key 리스트에 추가
 ```
 cat ~/.ssh/id_rsa.pub | sudo tee -a ~/.ssh/authorized_keys
 ```
 본 튜토리얼은 하나의 노드만 사용하므로 더이상의 구성은 필요하지 않으나, 여러개의 노드를 사용할 경우 상호 노드 간 SSH 통신이 가능하게 해주어야 합니다. 자세한 내용은 다음 링크를 참고하세요. [Knowledge Center - SSH Key 설정하기](https://www.ibm.com/support/knowledgecenter/SSBS6K_2.1.0.3/installing/ssh_keys.html)

 7. `/opt/ibm-cloud-private-ce-2.1.0.3/cluster/hosts` 파일에 노드의 IP 주소 입력
 
 ```
 vi cluster/hosts
 ``` 

 hosts 파일 수정
 ```
[master]
169.56.89.226

[worker]
169.56.89.226

[proxy]
169.56.89.226

#[management]
#4.4.4.4

#[va]
#5.5.5.5
```

7. 클러스터 노드간 통신에 SSH 키를 사용하기 위해 `/opt/cluster` 폴더에 `ssh_key` 파일을 덮어씀
```
sudo cp ~/.ssh/id_rsa ./cluster/ssh_key
```
 
### Step 3: 클러스터 설치 옵션
`cluster/config.yaml` 파일 설정을 통해 ICP 설치시 다양한 옵션 부여 

```
vi cluster/config.yaml
```

1. 모니터링, 미터링 서비스 활성화 
< 예시 라인 넣기!!>
2. 로깅 서비스 활성화 
```
kibana_install: true
``` 
<그림>

3. 그 외 ... (추가하기)

------------------------ 약 15분 소요

## Step 4: ICP 설치 
1. 설치 디렉토리 내 `cluster` 폴더로 이동 
```
cd ./cluster
```
2. ICP 클러스터 설치 
```
sudo docker run --net=host -t -e LICENSE=accept \
-v "$(pwd)":/installer/cluster ibmcom/icp-inception:2.1.0.3 install
```

3. 설치가 성공적으로 완료시 아래와 같이 뜹니다. 
```
UI URL is https://master_ip:8443 , default username/password is admin/admin
```

여기서 `master_ip`는 ICP master node의 IP 주소로, 실습 환경으로 부여받은 VM 의 IP와 같습니다. 

자, 이제 나만의 Kubernetes 환경이 여러가지 관리 서비스와 함께 설치 되었습니다. 
UI URL에 접속하여 대시보드를 둘러보세요!

