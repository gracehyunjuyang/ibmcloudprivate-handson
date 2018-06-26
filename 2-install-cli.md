### 1. kubectl 설치하기
```
docker run -e LICENSE=accept --net=host -v /usr/local/bin:/data ibmcom/icp-inception:2.1.0.3 cp /usr/local/bin/kubectl /data
```
[kubectl 링크](https://www.ibm.com/support/knowledgecenter/SSBS6K_2.1.0.3/manage_cluster/cfc_cli.html)

### 2. IBM Cloud Private CLI 설치하기
#### 2-1 IBM Cloud CLI 설치
1. tar 파일 풀기 
```
tar -xvf IBM_Cloud_CLI_0.7.1_amd64.tar.gz
``` 
2. 설치 파일 실행
```
cd Bluemix_CLI/
./install_bluemix_cli
```
3. IBM Cloud CLI 설치 여부 확인 
```
bx --help
``` 

#### 2-2 IBM Cloud Private 플러그인 설치 
1. 플러그인 설치 
```
bx plugin install /install/icp-linux-amd64
```
2. 플러그인 설치 완료 여부 확인
```
bx pr --help
```

<!--3. 클러스터에 로그인
```  
bx pr login -a https://<master_ip_address>:8443 --skip-ssl-validation
```-->

https://www.ibm.com/support/knowledgecenter/SSBS6K_2.1.0.3/manage_cluster/install_cli.html

## 3. Helm CLI 설치하기
### 3-1 Helm CLI 설치하기 
1. Helm 설치 바이너리 파일 다운로드 
```
docker run -e LICENSE=accept --net=host -v /usr/local/bin:/data ibmcom/icp-helm-api:1.0.0 cp /usr/src/app/public/cli/linux-amd64/helm /data
```

<!--Not applicable in 2.1.0.3-->
<!--2. Helm 실행 파이너리 파일을 PATH에 추가 
```
export HELM_HOME=/root/.helm
mv helm /usr/local/bin
```-->

2. kube-system 네임스페이스에 접근할 수 있도록 하는 certificate 을 제공  
  
  1. IBM Cloud Private CLI로 클러스터에 로그인 
 
  여기서 mycluster.icp는 곧 Master Node 의 IP주소 입니다. 
  ```
  bx pr login -a https://mycluster.icp:8443 --skip-ssl-validation
  ```

  2. 클러스터 사용자 계정으로 로그인 
  ```
  Username > admin
  Password > admin
  ```

  3. 클러스터 계정 선택하기
  ```
  Enter a number> 1
  ```
  클러스터 설정시, `cert.pem`과 `key.pem` 증명서가 `~/.helm` 디렉토리에 추가됩니다. 


### Helm 설치 여부 확인 
1. Helm CLI 초기화 
```
helm init --client-only
```

2. Helm CLI 가 초기화 되었음을 확인
```
helm version --tls
```

<!--### Helm 사용하기 
1. Helm repository 추가  (예. Kubernetes Incubater repo)
```
helm repo add incubator https://kubernetes-charts-incubator.storage.googleapis.com/
```

2. 사용 가능한 패키지 확인 
``` 
helm search -l
```

3. Helm 패키지 설치 (예. stable respository의 wordpress 패키지)  
```
helm install --name=my-wordpress stable/wordpress --tls
```

4. 설치된 패키지 리스팅 
``` 
helm list --tls
```

5. 설치된 패키지 삭제
``` 
helm delete my-wordpress --purge --tls
```

-->

<!--https://asciinema.org/a/czn4lLjC0ZEQYfG19d1e7MIL9 -->


