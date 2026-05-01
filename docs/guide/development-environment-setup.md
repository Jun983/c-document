# 개발 환경 설정

[README로 돌아가기](../../README.md)

이 문서는 **컴퓨터·프로그래밍을 처음 다루는 분**도 따라 할 수 있도록, Windows에서 **WSL**(리눅스 환경), **GCC**(C 언어 컴파일러), **Visual Studio Code**(편집 프로그램)를 설치하는 순서를 적었습니다.  
어려운 말은 최대한 줄이고, **복사해서 붙여 넣을 수 있는 명령**을 중심으로 설명합니다.

---

## 이 문서를 쓰기 전에

- **명령**이란, 검은 창(터미널)에 글자를 입력하고 **Enter**를 눌러 컴퓨터에게 시키는 말입니다. 아래 회색 박스 안의 글자를 **전부 선택해 복사**한 뒤, 터미널 창을 클릭하고 **붙여 넣기(Ctrl+V)** 한 다음 Enter를 누르면 됩니다.
- 설치 중에 **컴퓨터를 다시 시작하라**는 메시지가 나오면, 저장할 작업을 마친 뒤 재부팅해도 괜찮습니다.
- 중간에 **암호**를 물어보면, 키보드로 입력할 때 **화면에 글자가 안 보이는 경우가 많습니다**. 그래도 입력은 되고 있으니, 천천히 치고 Enter를 누르면 됩니다(리눅스에서 흔한 동작입니다).

---

## 자주 쓰는 도구: PowerShell이란?

**PowerShell**은 Windows에 기본으로 있는 **명령을 입력하는 창**입니다. 이 문서에서는 설치 확인·일부 설치를 PowerShell에서 진행합니다.

### PowerShell 여는 방법 (일반)

1. 키보드에서 **Windows 키**를 누릅니다.
2. **powershell** 이라고 입력합니다.
3. 목록에서 **Windows PowerShell** 또는 **PowerShell**을 눌러 실행합니다.

### 관리자 권한으로 PowerShell 여는 방법

일부 작업(WSL 처음 설치 등)은 **관리자 권한**이 필요합니다. 관리자 권한이란, “이 컴퓨터의 중요한 설정을 바꿀 수 있는 모드”라고 생각하면 됩니다.

1. **Windows 키**를 누릅니다.
2. **powershell** 이라고 입력합니다.
3. **Windows PowerShell** 항목에서 **마우스 오른쪽 버튼**을 누릅니다.
4. **관리자 권한으로 실행**을 선택합니다.
5. “이 앱이 디바이스를 변경하도록 허용하시겠습니까?” 같은 창이 나오면 **예**를 누릅니다.

창 제목 표시줄이나 내용에 **“관리자”**라는 말이 보이면 관리자 모드로 연 것입니다.

> **팁:** Windows 11에서는 시작 메뉴에서 **터미널**을 검색한 뒤, 마우스 오른쪽 버튼 → **관리자 권한으로 실행**을 선택해도 됩니다. 그다음 터미널 안에서 **PowerShell** 탭을 고르면 됩니다.

---

## 개요 (무엇을 하게 되나요?)

- **WSL** 안에서 **GCC**로 C 코드를 만들고 실행합니다.
- **VS Code**는 Windows에 설치하고, **WSL용 확장**을 써서 WSL 안의 폴더를 편집합니다.
- 파일은 가능하면 **WSL 안쪽 폴더**(예: 내 홈 폴더 아래)에 두면, Windows 디스크(`C:`)를 통해서 접근할 때보다 보통 더 빠릅니다.

## 전제 조건

- **Windows 10**(2004 이후 버전) 또는 **Windows 11**. 가능하면 **WSL 2**를 씁니다.
- **인터넷**에 연결되어 있어야 합니다(다운로드가 필요합니다).
- WSL을 **처음** 깔 때는 위에서 설명한 대로 **관리자 권한 PowerShell**이 필요할 수 있습니다.

---

## 1. WSL (Ubuntu 포함)

**WSL**은 Windows 안에서 가볍게 리눅스를 쓰게 해 주는 기능입니다. 여기서는 **Ubuntu**라는 배포판을 받아서 쓰는 방법을 안내합니다.

### 1-1. 이미 설치되어 있는지 확인 (일반 PowerShell)

관리자가 아니어도 되는 **일반 PowerShell**을 연 뒤, 아래를 복사해 실행합니다.

```powershell
wsl --list --verbose
```

- **Ubuntu** 같은 이름이 보이고, `STATE`가 `Running` 또는 `Stopped`이면 WSL과 리눅스가 이미 들어 있는 것입니다.
- `VERSION`이 **2**인지 봅니다. **1**이면 나중에 [WSL 2로 바꾸는 방법](https://learn.microsoft.com/windows/wsl/basic-commands#set-wsl-2-as-the-default-version)을 검토하면 좋습니다.

`wsl`이라고 쳤을 때 “명령을 찾을 수 없습니다”처럼 나오면, 아직 WSL이 준비되지 않은 경우가 많습니다.

추가로 상태만 보고 싶다면:

```powershell
wsl --status
```

### 1-2. 설치할 수 있는 Ubuntu 목록 보기

인터넷에서 받을 수 있는 배포판 목록을 보려면:

```powershell
wsl --list --online
```

목록에 **Ubuntu**가 있는지 확인할 수 있습니다.

### 1-3. Ubuntu를 지정해서 설치 (필요할 때만)

WSL을 **아직 안 깔았거나**, Ubuntu가 없다면 **관리자 권한 PowerShell**을 연 뒤 아래를 실행합니다.

```powershell
wsl --install -d Ubuntu
```

- `-d Ubuntu`는 **Ubuntu를 받아서 설치하겠다**는 뜻입니다.
- 예전에 `wsl --install`만 쓰던 방식과 비슷하지만, **배포판 이름을 Ubuntu로 분명히 적는** 방법입니다.

설치가 끝난 뒤 **재부팅을 하라**는 안내가 나오면, 안내에 따라 재부팅합니다.

> 이미 WSL만 있고 Ubuntu가 없다면, 관리자 PowerShell에서 `wsl --install -d Ubuntu`로 Ubuntu를 추가할 수 있는 경우가 많습니다. 이미 다른 방식으로 쓰고 있다면 [Microsoft WSL 설치 안내](https://learn.microsoft.com/windows/wsl/install)를 함께 보세요.

### 1-4. 처음 Ubuntu를 켰을 때

- **시작 메뉴**에서 **Ubuntu**를 찾아 실행하거나, PowerShell에 `wsl` 또는 아래처럼 입력합니다.

```powershell
wsl -d Ubuntu
```

- 처음에는 **리눅스 사용자 이름**과 **암호**를 정하라고 나옵니다. 이 암호는 나중에 `sudo` 명령(관리자 권한으로 설치할 때)에 쓰이니, **잊어버리지 않게** 적어 두는 것이 좋습니다.

---

## 2. WSL(리눅스) 안으로 들어가기

GCC 설치는 **반드시 WSL 안**, 즉 **Ubuntu 창**에서 합니다. Windows PowerShell이 아니라, **검은 창의 프롬프트가 리눅스처럼 보이는 곳**이어야 합니다.

### WSL(Ubuntu) 여는 방법

아래 중 편한 방법 하나만 쓰면 됩니다.

| 방법 | 설명 |
|------|------|
| **시작 메뉴** | “Ubuntu”를 검색해 **Ubuntu** 앱 실행 |
| **PowerShell에서** | `wsl` 입력 후 Enter, 또는 `wsl -d Ubuntu` 입력 후 Enter |
| **실행(Win+R)** | `wsl` 입력 후 Enter |

프롬프트에 보통 **사용자 이름**과 **`~`**(홈 폴더) 같은 표시가 나오고, Windows의 `C:\Users\...` 같은 긴 경로와는 다르게 보입니다. 그 상태가 **WSL에 들어온 것**입니다.

앞으로 이 문서에서 **“WSL 터미널”**이라고 하면, 위와 같이 연 **Ubuntu(리눅스) 창**을 말합니다.

---

## 3. GCC 및 빌드 도구 (WSL 안에서만)

**GCC**는 C 언어로 적은 글을 컴퓨터가 이해하는 형태로 바꿔 주는 도구입니다. **build-essential**이라는 묶음을 설치하면 GCC와 함께 자주 쓰는 도구가 같이 설치됩니다.

### 3-1. 이미 설치되어 있는지 확인 (WSL 터미널)

Ubuntu 창에서 아래를 **한 줄씩** 실행합니다.

```bash
gcc --version
```

버전 번호가 길게 나오면 이미 설치된 것입니다.

```bash
which gcc
```

`/usr/bin/gcc` 같은 경로가 나오면 정상입니다.

원하면 패키지 이름도 확인할 수 있습니다.

```bash
dpkg -l build-essential 2>/dev/null | head -n 3
```

### 3-2. 설치 (필요할 때만)

아래에서 **`sudo`**는 “관리자 권한으로 실행”이라는 뜻입니다. 암호를 물어보면, **WSL을 처음 만들 때 정한 리눅스 암호**를 입력합니다(입력할 때 글자가 안 보여도 됩니다).

```bash
sudo apt update
sudo apt install -y build-essential
```

`apt update`는 설치 가능한 프로그램 목록을 최신으로 맞추는 단계이고, 그다음 줄이 GCC 등을 실제로 깔아 넣는 단계입니다.

### 3-3. 동작 확인

```bash
gcc --version
```

간단히 컴파일이 되는지 테스트합니다.

```bash
echo 'int main(void) { return 0; }' > /tmp/t.c && gcc /tmp/t.c -o /tmp/t && /tmp/t && echo OK
```

마지막에 **OK**가 나오면 성공입니다.

---

## 4. Visual Studio Code (PowerShell로 확인·설치)

**Visual Studio Code**(줄여서 VS Code)는 코드를 편집하는 프로그램입니다. Windows에 설치하고, 앞에서 설치한 **WSL과 연결**해서 쓰는 방식입니다.

### 4-1. 이미 설치되어 있는지 확인 (PowerShell)

일반 PowerShell에서 아래를 실행합니다.

```powershell
@(
  "$env:LocalAppData\Programs\Microsoft VS Code\Code.exe",
  "$env:ProgramFiles\Microsoft VS Code\Code.exe"
) | ForEach-Object { if (Test-Path $_) { "Found: $_" } }
```

`Found:`로 경로가 나오면 VS Code 프로그램이 있는 것입니다.

터미널에서 **`code`**라는 짧은 명령을 쓸 수 있는지 확인합니다.

```powershell
Get-Command code -ErrorAction SilentlyContinue
```

무언가 출력되면 `code` 명령을 쓸 준비가 된 것입니다.

### 4-2. 설치 (필요할 때만, PowerShell)

**winget**(Windows에 있는 패키지 관리자)이 있으면, PowerShell에서:

```powershell
winget install -e --id Microsoft.VisualStudioCode
```

winget이 없으면(예: `winget` 명령 인식 실패), **PowerShell에서 Microsoft Store 앱 설치 프로그램(App Installer) 페이지를 열어** 설치할 수 있습니다:

```powershell
Start-Process "ms-windows-store://pdp/?ProductId=9NBLGGH4NNS1"
```

Store 화면이 열리면 **설치**를 누릅니다. 설치가 끝난 뒤 PowerShell을 닫았다가 다시 열고 아래로 확인합니다.

```powershell
winget --version
```

그래도 winget을 쓸 수 없으면, 브라우저로 [Visual Studio Code 공식 사이트](https://code.visualstudio.com/)에 들어가 **Windows용 설치 파일**을 받아 실행합니다. 설치 마법사의 안내를 따라가면 됩니다.

설치 후 **PowerShell 창을 닫았다가 다시 연 다음**, 다시 `Get-Command code`로 확인합니다.  
`code`가 없으면 VS Code를 한 번 실행한 뒤, 키보드 **Ctrl+Shift+P**를 누르고 **“Shell Command: Install 'code' command in PATH”**라는 항목을 찾아 실행합니다(영문 메뉴일 수 있습니다).

### 4-3. 확장 설치 (PowerShell)

VS Code가 설치된 상태에서, **새 PowerShell**에 아래를 입력합니다.

```powershell
code --install-extension ms-vscode-remote.remote-wsl
code --install-extension ms-vscode.cpptools
```

이미 깔린 확장은 알아서 건너뜁니다. 목록을 보려면:

```powershell
code --list-extensions
```

### 4-4. WSL 폴더를 VS Code로 열기

1. 먼저 **WSL(Ubuntu)** 창에서 작업할 폴더로 이동합니다(예: `cd ~` 는 홈 폴더로 이동).
2. 그 폴더에서 아래를 실행합니다.

```bash
code .
```

WSL용 확장이 있으면 VS Code가 **WSL에 연결된 상태**로 그 폴더를 엽니다.

또는 VS Code에서 **파일 → 폴더 열기**로 `\\wsl$\Ubuntu\home\본인사용자이름\...` 형태의 경로를 선택할 수 있습니다(`Ubuntu`는 설치한 이름에 맞게 바꿉니다).

---

## 문제 해결

| 증상 | 확인할 것 |
|------|-----------|
| `gcc: command not found` | 명령을 **Ubuntu(WSL) 창**에서 쳤는지 확인합니다. Windows PowerShell에서는 `gcc`가 동작하지 않을 수 있습니다. `build-essential` 설치도 다시 확인합니다. |
| VS Code가 WSL과 연결되지 않음 | `ms-vscode-remote.remote-wsl` 확장이 설치되었는지, `wsl -l -v`에 Ubuntu가 있는지 봅니다. |
| `code` 명령 없음 | VS Code 설치 여부, PATH, **Shell Command: Install 'code'…** 실행 여부 |
| `/mnt/c/...` 쪽만 느림 | 프로젝트를 WSL 홈 아래 등 **리눅스 쪽 폴더**로 옮겨 보세요. |

더 자세한 설명은 [WSL 공식 문서](https://learn.microsoft.com/windows/wsl/), [VS Code와 WSL](https://code.visualstudio.com/docs/remote/wsl)을 참고하면 좋습니다.
