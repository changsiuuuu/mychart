## helmchart 만들고 github pages로 배포

## 작성한 chart가 잘 실행되는지 확인
```bash
[user1@master charts]$ helm ls -n helm01
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS       CHART                   APP VERSION
member-release  helm01          1               2026-06-29 10:34:20.088786988 +0900 KST deployed     member-app-0.1.0

[user1@master charts]$ k get pod,svc -n helm01
NAME                              READY   STATUS    RESTARTS   AGE
pod/member-app-75d88b9d98-bbmcs   1/1     Running   0          2m41s
pod/member-app-75d88b9d98-dg998   1/1     Running   0          2m41s
pod/member-app-75d88b9d98-lt747   1/1     Running   0          2m41s

NAME                         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
service/member-app-service   ClusterIP   10.101.46.75   <none>        8000/TCP   2m41s
```


### 작성한 helm chart 코드를 깃헙에 푸시한다
```bash
[user1@master mychart]$ git add .
[user1@master mychart]$ git commit -m "helm01_member"

[user1@master mychart]$ git remote add origin <원격 저장소>
[user1@master mychart]$ git push -u origin master
```

### docs 폴더 구성
```bash
# docs 폴더 생성
mkdir -p docs
# 만든 chart를 압축해서 docs/ 폴더 안에 저장
helm package charts/helm01_member -d docs/

# index.yaml 파일을 docs 폴더에 생성하기
helm repo index docs/ --url https://changsiuuuu.github.io/mychart
```

### push 하고 페이지 설정하면 배포가된다
# branch -> master -> /docs
세이브 누르고 actions 보면 뭔가 동작을한다
pages build and deployment 이 자동으로 수행

다음에 새로운 chart를 추가하거나 기존 chart를 수정해서 /docs 안에 내용을 업데이트 한 후에 master 브랜치로  push 하면 이 동작은 자동으로 실행된다.