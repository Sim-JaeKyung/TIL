# gitignore

>  git으로 관리하고 싶지 않은 파일들의 리스트를 작성하여,
>
> 특정 파일들을 git이 버전 관리를 하지 않도록 하는 것

```bash
touch .gitignore.txt
```

> 텍스트 파일 gitignore을 생성한 뒤 자바로 실행.
>
> Stagina area로 넘기기 싫은 파일 목록들, 건드리면 안되는 파일 목록들을 작성

- 일반적으로 개인정보 및 특정 사람에게만 적용되는 환경들(개인 개발환경 관련)이 이 파일에 작성됨
- 개발환경 관련 파일들(.idea 등)은 버전관리가 될 필요도 없을 뿐더러, 개인정보 같은건 애초에 GitHub에 올라가서는 안됨
- [Gitignore.io](https://gitignore.io/) 
  - 본인 개발 환경에 대한 내용(ex. windows, mac os, eclipes etc..)을 넣고 생성하면, 일반적으로 개발자들이 많이 쓰는 gitignore 문서를 제공

> git init 후 첫 add 전에 작성하는 것

