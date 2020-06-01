---
title: "Git에서 Untracked 상태인 파일 삭제하기"
categories:
  - Git
tags:
  - Git
---

작업 도중 실수로 수정내역을 Add했을 때 Add 상태를 되돌릴 수 있다. 

```bash
$ git reset HEAD [file]
```

이렇게 특정 파일을 `reset` 하면 Stage 상태에 추가(Add)되어 Commit을 기다리던 파일이 Unstaged 상태가 되며, 수정했던 내용은 그대로 워킹 디렉토리에 보존된다.
특정 파일이 아니라 전체를 취소하려면 파일명(패스)를 작성하지 않는다.
