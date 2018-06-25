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
./install_bluemix
```
3. IBM Cloud CLI 설치 여부 확인 
```
bx --help
``` 

#### 2-2 IBM Cloud Private 플러그인 설치 
1. 플러그인 설치 
``` 
bx plugin install /<path_to_installer>/<cli_file_name>
```
2. 플러그인 설치 완료 여부 확인
```
bx pr --help
```

3. 클러스터에 로그인
```  
bx pr login -a https://<master_ip_address>:8443 --skip-ssl-validation
```

https://www.ibm.com/support/knowledgecenter/SSBS6K_2.1.0.3/manage_cluster/install_cli.html

## 3. Helm CLI 설치하기
