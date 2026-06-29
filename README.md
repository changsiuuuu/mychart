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

