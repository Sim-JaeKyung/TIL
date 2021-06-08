[toc]

# undoing

> 원상태로 되돌리기

**사전 준비**

```bash
$ mkdir undoing
$ cd undoing
$ touch a.txt README.md
```

<br>

## 1. 파일 상태를 Unstage로 변경하기

> - Staging Area와 Worink Directory 사이를 넘나드는 방법

![areas](c:/my_dir/git_class/md-images/1.jpg)

<br>

### 첫번째

> ```bash
> $ git rm --cached <file>
> ```
>
> - 따로 따로 커밋하려고 했지만, 실수로 `git add .` 이라고 실행해 버린 상황
>
> - 처음으로 add 된 상황

```bash
$ git init
$ git add .
```

```bash
$ git status

On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
        new file:   a.txt
```

```bash
# a.txt를 unstage

$ git rm --cached a.txt
```

```bash
$ git status

On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.txt
```

<br>

**두번째 실습 전 사전 준비**

```bash
$ git add .
$ git commit -m "first commit"
```

<br>

### 두번째

> ```bash
> $ git restore --staged <file>
> ```
>
> 두 개의 파일을 모두 수정하고서 따로따로 커밋하려고 했지만, 
> 실수로 `git add .` 라고 실행해 버린 상황

```bash
$ git add .
```

```bash
$ git statusOn branch masterChanges to be committed:  (use "git restore --staged <file>..." to unstage)        modified:   README.md        modified:   a.txt
```

```bash
# a.txt를 unstage$ git restore --staged a.txt
```

```bash
$ git statusOn branch masterChanges to be committed:  (use "git restore --staged <file>..." to unstage)        modified:   README.mdChanges not staged for commit:  (use "git add <file>..." to update what will be committed)  (use "git restore <file>..." to discard changes in working directory)        modified:   a.txt
```

<br>

### 첫번째와 두번째 상황에서 명령어가 다른 이유

> 1. `git rm --cached <file>`
>    - 기존에 커밋이 없는 경우
>    - to unstage and remove paths only from the staging area
> 2. `git restore --staged <file>`
>    - 기존에 커밋이 존재하는 경우
>    - the contents are restored from `HEAD`

<br>

---

<br>

## 2. Modified 파일 되돌리기

> ```bash
> $ git restore <file>
> ```
>
> (add가 되어있지 않은, working derictory에 있는)
>
> 수정된 a.txt를 다시 되돌리기
>
> [주의 사항] 
>
> - 원래 파일로 덮어썼기 때문에 수정한 내용은 전부 사라짐
> - 수정한 내용이 진짜 마음에 들지 않을 때만 사용
> - 즉, 해당 명령어를 실행한 이후 절대로 다시 복원 불가능

```bash
$ git statusOn branch masterChanges to be committed:  (use "git restore --staged <file>..." to unstage)        modified:   README.mdChanges not staged for commit:  (use "git add <file>..." to update what will be committed)  (use "git restore <file>..." to discard changes in working directory)        modified:   a.txt
```

```bash
$ git restore a.txt
```

```bash
$ git statusOn branch masterChanges to be committed:  (use "git restore --staged <file>..." to unstage)        modified:   README.md
```

<br>

---

<br>

## 3. 완료한 커밋 수정

> ```bash
> $ git commit --amend
> ```
>
> 1. 커밋 메시지를 잘못 적었을 때
> 2. 너무 일찍 커밋했거나 (어떤 파일을 빼먹었을 때)
>
> [주의 사항]
>
> - 공개된 저장소에 push 된 커밋 메세지는 절대 수정하지 말기
> - 커밋 해시값이 변경되기 때문!!!

<br>

### 3-1 커밋 메세지 수정

> 마지막으로 커밋하고 나서 수정한 것이 없다면 
> (커밋하자마자 바로 이 명령을 실행하는 경우)
>
> 이때는 커밋 메시지만 수정함

```bash
$ git add .$ git commit -m "test"[master b0a352d] test 1 file changed, 1 insertion(+) create mode 100644 asd.txt
```

```bash
$ git commit --amendhint: Waiting for your editor to close the file..[master c01f908] Add no.txt Date: Fri Jun 4 17:21:43 2021 +0900 1 file changed, 0 insertions(+), 0 deletions(-) create mode 100644 asd.txt
```

* 설정에 따라 visual studio code나 vim 등 커밋 메시지 작성 화면이 나옴
* 여기에서 커밋 메세지를 수정하고 저장하면 반영 됨

<br>

### 3-2 어떤 파일을 빼먹었을 때

> 다시 커밋하고 싶으면 파일 수정 작업을 하고 Staging Area에 추가한 다음 
>
> `--amend` 옵션을 사용하여 커밋을 재작성

```bash
$ touch foo.txt bar.txt$ git add foo.txt
```

```bash
$ git statusOn branch masterChanges to be committed:  (use "git restore --staged <file>..." to unstage)        new file:   foo.txtUntracked files:  (use "git add <file>..." to include in what will be committed)        bar.txt$ git statusOn branch masterUntracked files:  (use "git add <file>..." to include in what will be committed)        omit.txtnothing added to commit but untracked files present (use "git add" to track)
```

```bash
# 실수로 bar.txt를 빼고 커밋 함$ git commit -m "foo & bar"[master 4221af6] foo & bar 1 file changed, 0 insertions(+), 0 deletions(-) create mode 100644 foo.txt
```

```bash
$ git statusOn branch masterUntracked files:  (use "git add <file>..." to include in what will be committed)        bar.txt
```

<br>

**해결하기**

```bash
$ git add bar.txt$ git statusOn branch masterChanges to be committed:  (use "git restore --staged <file>..." to unstage)        new file:   bar.txt$ git commit --amendhint: Waiting for your editor to close the file..[master ce77c2d] omit & real Date: Fri Jun 4 17:29:22 2021 +0900 2 files changed, 0 insertions(+), 0 deletions(-) create mode 100644 omit.txt create mode 100644 real.txt
```

```bash
$ git statusOn branch masterChanges to be committed:  (use "git restore --staged <file>..." to unstage)        new file:   bar.txt
```

```bash
# 커밋 편집기 활성화 됨$ git commit --amendfoo & bar# Please enter the commit message for your changes. Lines starting# with '#' will be ignored, and an empty message aborts the commit.## Date:      Mon Jun 7 22:32:58 2021 +0900## On branch master# Changes to be committed:#       new file:   bar.txt#       new file:   foo.txt
```

- 저장 후 종료

  ```bash
  $ git commit --amend[master 7f6c24c] foo & bar Date: Mon Jun 7 22:32:58 2021 +0900 2 files changed, 0 insertions(+), 0 deletions(-) create mode 100644 bar.txt create mode 100644 foo.txt
  ```

  - `create mode 100644 bar.txt` 가 추가된 것을 확인
  - commit은 새로 추가되지 않았음

  