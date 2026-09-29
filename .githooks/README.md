# 커밋 전 비밀값 검사

저장소를 새로 복제한 뒤 루트에서 한 번 실행합니다.

```sh
brew install gitleaks
sh .githooks/install
```

macOS 이외 환경에서는 [공식 설치 안내](https://github.com/gitleaks/gitleaks#installing)에 따라 gitleaks를 설치한 뒤 같은 설치 스크립트를 실행합니다.

스테이징한 변경에서 비밀값을 탐지하면 커밋이 중단됩니다. 검사 도구가 없거나 검사가 실패해도 커밋하지 않습니다. 기존 pre-commit은 `.git/hooks/pre-commit.before-gitleaks`에 보존하고 먼저 호출합니다. 기존 훅이 스테이징 내용을 바꾸는 경우까지 검사하도록 gitleaks를 마지막에 실행합니다. Entire의 다른 Git 훅과 `core.hooksPath`는 변경하지 않습니다.

GitHub의 `Gitleaks` 검사도 push 및 pull request의 새 커밋을 검사합니다. 수동 실행은 현재 브랜치 전체 이력을 검사합니다. 탐지된 값은 로그에서 가립니다. CI 실행에는 저장소 설정 파일을 GitHub에 푸시해야 합니다. 브랜치 보호의 필수 검사 지정은 별도 저장소 정책입니다.
