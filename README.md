# gitops-template

`kustomization.yaml` 기반 gitops template

### package structure
```
ㄴ base
  ㄴ kustomization.yaml
  ㄴ manifest.yaml
ㄴ overlays
  ㄴ dev
    ㄴ ingress.yaml
    ㄴ kustomization.yaml
  ㄴ prod
    ㄴ ...
```

- base 경로를 기본으로 두고, overlays 하위에 각 배포 환경별 resource를 구성한다.
- 이 Github Repository엔 배포 대상 서비스의 Docker Image, Kubernetes 형상이 들어가지 않는다.
  - 배포 형상 관리용 Github Repository는 별도로 존재하며 이 저장소에 tag or release를 기반으로 배포 대상 서비스의 artifact 형상이 올라간다. → 이를 기반으로 ArgoCD에서 CD를 수행한다.
  - 서비스에서 사용되는 라이브러리는 사설 Nexus Repository를 바라보도록 한다. (eg. `build.gradle`)
  - 서비스에 대한 CI 결과로 Docker Image는 Harbor에 올라간다.