# 📋 명령어 보관함

관리자(세해)가 등록한 GPT·Claude·Gemini 프롬프트를 여러 사람이 보고 복사해서 쓰는 휴대폰 앱입니다.

## 누가 무엇을 할 수 있나요
| | 보기 · 분류 · 복사 | 등록 · 수정 · 삭제 |
|---|---|---|
| 사용자 (앱을 받은 모든 사람) | ✅ | ❌ (버튼 자체가 없음) |
| 관리자 (GitHub 토큰을 넣은 휴대폰) | ✅ | ✅ |

- 데이터는 이 GitHub 저장소의 `data/prompts.json`, 이미지는 `data/images/` 폴더에 저장됩니다.
- 관리자가 저장하면 GitHub에 기록 → Vercel이 자동으로 다시 배포 → **1~2분 뒤** 모든 사용자 화면에 반영됩니다.
- GitHub에 모든 변경 기록이 남아서, 실수로 지워도 GitHub에서 예전 버전을 찾을 수 있어요.

## 올릴 파일 (8개)
```
index.html
manifest.webmanifest
sw.js
icon-192.png
icon-512.png
icon-512-maskable.png
README.md
data/prompts.json      ← data 폴더째 올리기
```

---

## 1단계. GitHub에 올리기
1. https://github.com 로그인 → 오른쪽 위 **＋ → New repository**
2. Repository name: `gpt-prompt-app` → **Create repository**
3. **uploading an existing file** 클릭
4. zip을 푼 `gpt-prompt-app` 폴더 **안의** 파일들과 `data` 폴더를 한꺼번에 끌어다 놓기
   - 업로드 목록에 `data/prompts.json`이 보이면 정상
5. **Commit changes**

## 2단계. Vercel로 배포하기
1. https://vercel.com → **Continue with GitHub**
2. **Add New… → Project** → `gpt-prompt-app` 옆 **Import** → **Deploy**
3. 생긴 주소(`https://gpt-prompt-app-xxxx.vercel.app`)를 휴대폰으로 열어 확인
4. 이 주소를 다른 사람들에게 공유하면 됩니다

## 3단계. 관리자 토큰 만들기 (세해님만, 한 번)
1. GitHub 오른쪽 위 프로필 → **Settings**
2. 왼쪽 맨 아래 **Developer settings → Personal access tokens → Fine-grained tokens**
3. **Generate new token**
   - Token name: `명령어 보관함`
   - Expiration: 원하는 기간 (만료되면 새로 만들어 다시 입력)
   - Repository access: **Only select repositories** → `gpt-prompt-app` 선택
   - Permissions → Repository permissions → **Contents: Read and write**
4. **Generate token** → 나온 `github_pat_…` 값을 복사 (이 화면에서 한 번만 보여요)

## 4단계. 앱에서 관리자 모드 켜기
1. 앱 목록 맨 아래 작은 **🔒 관리자** 누르기
2. GitHub 아이디 / 저장소 이름(`gpt-prompt-app`) / 토큰 입력 → **관리자 모드 켜기**
3. 아래에 **📋 보기 / ✏️ 입력** 탭과 카드마다 **수정 · 삭제** 버튼이 생깁니다
4. 위쪽 **잠그기**를 누르면 관리자 모드가 꺼지고 토큰이 휴대폰에서 지워져요

> ⚠️ 토큰은 비밀번호와 같아요. 다른 사람에게 보내지 마세요.
> 잃어버리거나 유출됐다면 GitHub의 같은 화면에서 그 토큰을 **Delete** 하면 바로 무효가 됩니다.

### PC에서 입력하기 (작업량이 많을 때)
- PC 크롬에서 Vercel 주소를 열고, 똑같이 **🔒 관리자**에 같은 토큰을 넣으면 됩니다.
- PC에서는 **왼쪽 입력 / 오른쪽 목록**이 나란히 나오는 넓은 작업 화면이 돼요.
- 이미지는 칸에 **끌어다 놓기**, 또는 캡처 후 칸에 마우스를 올리고 **Ctrl+V**
- **Ctrl+Enter**로 바로 저장 → 제목 칸으로 돌아가서 다음 입력
- 휴대폰과 PC를 같이 관리자로 써도 됩니다. 다른 기기에서 저장한 내용은 새로고침하면 보여요.

## 5단계. APK 만들기 (PWABuilder)
1. https://www.pwabuilder.com 에 Vercel 주소 입력 → **Start**
2. **Package For Stores → Android → Generate Package → Download**
3. zip 안의 `.apk` 파일을 휴대폰으로 옮겨 설치 ("출처를 알 수 없는 앱" 허용)

> APK 없이도 안드로이드 크롬에서 주소를 열고 **⋮ → 홈 화면에 추가**를 누르면 앱처럼 설치돼요.

---

## 참고
- 목록이 안 보이면: 내려받은 `index.html`을 직접 열면 데이터가 안 보여요. 꼭 **Vercel 주소**로 열어 주세요.
- 저장할 때마다 Vercel이 새로 배포합니다. 무료 요금제는 하루 100번까지라 평소 사용에는 충분해요.
