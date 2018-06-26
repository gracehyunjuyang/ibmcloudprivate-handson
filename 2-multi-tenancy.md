## 사용자 관리 , 멀티 테넌시 

### 1. LDAP 연계 
IBM Cloud Privae 과 LDAP 연계에 대한 상세 내용은 아래 [IBM KnowledgeCenter](https://www.ibm.com/support/knowledgecenter/SSBS6K_2.1.0/user_management/configure_ldap.html) 참고
 
 1. LDAP의 IP와 port를 확보합니다. 저는 테스트 용도로 OpenLDAP을 사용합니다. 
 2. 플랫폼 대시보드 화면에서 ***Manage > Authentication*** 클릭 후 아래 내용을 입력
    #### LDAP Connection
    - Name: `ldap`
    - Type: `Custom`
    - URL: `ldap://<cluster-ip>:389`
    
    #### LDAP authentication
    - Base DN: `dc=local,dc=io` (default value, adjust as needed)
    - Bind DN: `cn=admin,dc=local,dc=io` (default value, adjust as needed)
    - Admin Password: `admin` (default value, adjust as needed)
    
    #### LDAP Filters
    - Group filter: `(&(cn=%v)(objectclass=groupOfUniqueNames))`
    - User filter: `(&(uid=%v)(objectclass=person))`
    - Group ID map: `*:cn`
    - User ID map: `*:uid`
    - Group member ID map: `groupOfUniqueNames:uniquemember`

    ***Save*** 합니다.
    
 3. LDAP에 만들어진 사용자(user) 혹은 그룹(group)을 team에 추가합니다. 대시보드에서 ***Manage > Teams*** 로 이동 
   - ***Create team*** 클릭
   - 추가할 group 혹은 사용자 이름을 검색하여 각 사용자에 적절한 역할을 할당합니다.
