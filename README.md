# PO:VE — PRE-OPENING

프리오프닝 랜딩 페이지. 정적 사이트이며 빌드 과정이 없습니다.

    index.html          페이지 본문 (HTML · CSS · JS 한 파일)
    pove-founder.js     대표원장 약력 데이터
    vercel.json         배포 설정 (clean URL · 캐시 · 보안 헤더)
    robots.txt          검색엔진 크롤링 안내
    sitemap.xml         검색엔진용 페이지 목록
    assets/
      og-image.png      카카오톡 · 인스타 공유 썸네일
      logo-*.svg        로고 (세로형 · 가로형)
      img/              사진 · 히어로 영상

---

## 배포 구조

    Claude (수정)  →  GitHub (main 브랜치)  →  Vercel (자동 배포)

- `main` 브랜치에 푸시 → **프로덕션** 자동 배포
- 다른 브랜치 푸시 · PR 생성 → **프리뷰 URL** 자동 생성 (실서비스 영향 없음)

## 최초 세팅 (한 번만)

### 1. GitHub에 올리기

저장소: https://github.com/donghyunkim-cpu/pove-test

저장소 첫 화면의 **uploading an existing file** 링크를 누르고, 이 폴더의 **내용물 전체**를
드래그합니다. (`deploy` 폴더 자체가 아니라 그 안의 파일들 — 폴더째 올리면 주소가
`/deploy/` 로 한 단계 들어갑니다.)

올릴 항목: `index.html` · `pove-founder.js` · `vercel.json` · `robots.txt` ·
`sitemap.xml` · `README.md` · `assets` 폴더

### 2. Vercel 연결

1. [vercel.com](https://vercel.com) → GitHub 계정으로 로그인
2. **Add New → Project** → 이 저장소 선택 → **Import**
3. Framework Preset: **Other** · Build Command: **비움** · Output Directory: **비움**
4. **Deploy**

여기까지 하면 `프로젝트명.vercel.app` 주소로 사이트가 열립니다.

### 3. 도메인 연결

Vercel 프로젝트 → **Settings → Domains** → 도메인 입력 → 안내되는 값(A 레코드 또는
CNAME)을 도메인 구입처(가비아 · 카페24 등) DNS 설정에 등록합니다.
HTTPS 인증서는 Vercel이 자동 발급합니다.

### 4. 도메인 확정 후 필수 작업

아래 3개 파일에서 `REPLACE-WITH-YOUR-DOMAIN` 을 실제 도메인으로 바꿉니다.
안 바꾸면 카카오톡 · 인스타로 링크를 공유할 때 썸네일이 뜨지 않습니다.

| 파일 | 위치 |
|---|---|
| `index.html` | og:image · og:url · canonical (3곳) |
| `robots.txt` | Sitemap 주소 |
| `sitemap.xml` | loc 주소 |

예: `https://REPLACE-WITH-YOUR-DOMAIN/` → `https://pove.co.kr/`

---

## 수정할 때

파일을 직접 고치지 말고 Claude에 요청하세요. 수정된 파일을 받아 GitHub에
덮어쓰기(같은 파일명으로 다시 업로드)하면 Vercel이 자동으로 재배포합니다.

문구 · 색 · 이미지 정도의 변경은 원본(`POVE Pre-Opening.dc.html`)에서 수정한 뒤
이 폴더를 다시 생성하는 방식으로 관리합니다.

## 주의

- 폴더 구조를 바꾸면 이미지 · 영상 경로가 깨집니다.
- 글꼴은 Google Fonts · Pretendard CDN에서 불러옵니다.
- 히어로 영상은 자동재생됩니다 (2.7MB · 모바일 데이터 고려한 용량).
- 배포에 문제가 생기면 Vercel → Deployments 에서 이전 배포를 **Promote to Production**
  으로 즉시 되돌릴 수 있습니다.
