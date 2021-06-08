# Branch command

- 브랜치 생성

```bash
$git branch 브랜치명
```

- 브랜치 목록

```bash
$git branch
```

- 브랜치 이동

```bash
$git checkout 브랜치명
or
$git switch 브랜드명
```

- 브랜치 생성 + 이동 

```bash
$git checkout -b 브랜치명
or
$git switch -c 브랜치명
```

- 브랜치 병합

```bash
(master) $git merge 브랜치명
```

- 브랜치 삭제

```bash
$git branch -d 브랜치명
$git branch -D 브랜치명
```

> d가 일반적인 삭제 옵션
>
> D는 강제 삭제 옵션
>
> merge가 되지 않은 브랜치는 강제로 삭제해야 함
>
> ```bash
> error: The branch 'hotfix' is not fully merged.
> If you are sure you want to delete it, run 'git branch -D hotfix'.
> ```
>
> 