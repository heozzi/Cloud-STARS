# ARGO 설치
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

- 안씀
kubectl apply -n default -f .\argo-install.yaml
```

# ARGO 패스워드 찾기
Powershell에서 실행
```
Base64로 인코딩된 비밀번호 확인 
kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}"

디코딩 하는 코드
[System.Text.Encoding]::UTF8.GetString([Convert]::FromBase64String("패스워드"))
[System.Text.Encoding]::UTF8.GetString([Convert]::FromBase64String("YTBzZ3JKa0U0VjRIYkN6R2pJV2VPVnVJRzhpMGhNME03Z0R1WTNrVkdIOURpNFpVZDNYeHlt"))
```

# 아르고 패스워드 변경
```
kubectl exec -it -n argocd deployment/argocd-server -- /bin/bash

argocd login localhost:8080 --username admin --password "디코딩패스워드" --insecure
argocd login localhost:8080 --username admin --password "98FlmgH9EhcktauZ" --insecure

argocd account update-password

```

# 포트포워딩으로 실행
```
kubectl port-forward svc/argocd-server -n argocd 8889:443
```


# 아르고 CD 배포 진행
```
kubectl apply -f efs-application.yaml -n argocd
kubectl apply -f spring-application.yaml -n argocd
kubectl apply -f jenkins-application.yaml -n argocd
kubectl apply -f ingress-application.yaml -n argocd
```