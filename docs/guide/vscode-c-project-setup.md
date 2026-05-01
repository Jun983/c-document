# Visual Studio Code로 C 언어 프로젝트 만들기

[처음 안내 페이지로 돌아가기](../../README.md)

이 문서는 VS Code와 WSL(Ubuntu) 환경에서 C 언어 프로젝트를 처음 만드는 방법을 단계별로 설명합니다.  
처음 배우는 분도 그대로 따라 하면, 프로젝트 생성부터 빌드/실행까지 완료할 수 있습니다.

---

## 준비 사항

먼저 아래가 설치되어 있어야 합니다.

- WSL(Ubuntu)
- GCC (`build-essential`)
- Visual Studio Code
- VS Code 확장: `Remote - WSL`, `C/C++`

설치가 아직이라면 아래 문서를 먼저 완료해 주세요.

- [개발 환경 설정 가이드](./development-environment-setup.md)

---

## 1. 프로젝트 폴더 만들기 (WSL 터미널)

WSL(Ubuntu) 터미널에서 아래를 실행합니다.

```bash
mkdir -p ~/c-workspace/test-project
cd ~/c-workspace/test-project
```

- `~/c-workspace`: C 프로젝트를 모아 두는 폴더
- `test-project`: 이번에 만들 프로젝트 폴더

---

## 2. VS Code로 폴더 열기

같은 WSL 터미널에서 아래를 실행합니다.

```bash
code .
```

그러면 VS Code가 WSL 연결 상태로 현재 폴더를 엽니다.

---

## 3. 기본 파일 만들기

프로젝트 루트(`test-project`)에 `main.c` 파일을 만들고 아래 코드를 넣습니다.

```c
#include <stdio.h>

int main(void) {
    printf("VS Code C Project Start!\n");
    return 0;
}
```

---

## 4. 터미널에서 빌드/실행 확인

VS Code 하단 터미널(WSL)에서 아래를 실행합니다.

```bash
gcc main.c -o app
./app
```

정상이라면 아래처럼 출력됩니다.

```text
VS Code C Project Start!
```

---

## 5. 추천 폴더 구조

작은 연습 프로젝트는 아래 구조로 시작하면 충분합니다.

```text
test-project/
└─ main.c
```

프로젝트가 커지면 `src/`, `include/`, `bin/` 폴더로 분리하면 좋습니다.

