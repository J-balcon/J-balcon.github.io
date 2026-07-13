# 정학영 애니메이션 포트폴리오 — 작업 기록

마지막 업데이트: 2026-07-13

## 사이트 정보

- 로컬 작업 파일: `index.html` (이 폴더)
- GitHub 저장소: `J-balcon/J-balcon.github.io`
- 정식 주소(정답): **https://j-balcon.github.io/portfolio/index.html**
- 옛 주소(오타, `portpolio`): 접속하면 위 정식 주소로 자동 리다이렉트되도록 처리해둠. 링크 공유 시 정식 주소 사용 권장.
- GitHub에 CLI/git 연결이 안 되어 있어서, 업데이트할 때마다 GitHub 웹사이트의 "Add file → Upload files" 화면에 `index.html`(또는 이미지)을 올리고 커밋하는 방식으로 배포함. 배포 후 CDN 캐시 반영에 1~2분 정도 걸릴 수 있음.

## 페이지 구조

```
<header class="hero">          — 첫 화면(이름, 소개, 이메일, 태그 버튼, 배경 슬라이드쇼)
<main>
  <section class="work">       — 좌우 두 컬럼(사선 분할)
    <div class="col toon">     — 01 CARTOON / TOON SHADER
    <div class="col real">     — 02 REALISTIC / PHYSICAL WEIGHT
<footer>                       — 연락처
```

### 인터랙션
- 컬럼에 마우스를 올리거나 클릭하면 그쪽이 확장됨. 클릭하면 고정(잠금)되고, 같은 곳을 다시 클릭하면 해제.
- 영상은 클릭 전엔 썸네일+재생버튼(파사드) 상태로만 보이고, 클릭해야 실제 유튜브 iframe이 로드되며 재생됨(초기 로딩을 가볍게 하고 유튜브 UI 노출을 막기 위함).
- 한쪽 영상이 재생되면 그 컬럼이 확장 고정되고, 반대쪽 영상을 재생하면 이전 영상은 자동 정지되고 확장이 넘어감.
- 히어로 배경은 30장의 이미지가 4초 간격으로 서서히 디졸브되며 순환됨(한 바퀴 도는 데 2분 정도).
- 영상 컬럼에 마우스만 올렸을 때 커졌다 작아졌다 하는 호버 확장 효과는 제거함(어지럽다는 피드백) — 클릭으로만 확장/고정됨.

## 현재 채워진 콘텐츠

- 이름: HAKYOUNG JEONG / 정학영
- 소개 문구(4줄 고정 — 화면 크기와 무관하게 이 줄바꿈 유지됨):
  ```
  Character Animator / 10 Years — Locus Studio · Lennon Studio 출신.
  프리비즈부터 파이널까지
  카투니 스타일라이즈드와 리얼리스틱 모캡 애니메이션을 넘나들며
  크리쳐와 캐릭터에 생명력을 불어넣습니다.
  ```
- 연락처: goodgkrdud@gmail.com (히어로 + 푸터 두 곳)
- 태그 버튼 텍스트: "TOON SHADER" → "CARTOON STYLE"로 변경됨(섹션 제목/aria-label도 동일하게 변경)
- CARTOON STYLE 영상: 유튜브 ID `clMdal8VOGQ`
- PHYSICAL WEIGHT 영상: 유튜브 ID `X_EfCIHTrwE`
- 히어로 배경 슬라이드(2026-07-13 교체 — 실제 릴 프레임 30장 전부, 카투니/실사 번갈아 배치):
  - `images/hero/hero-01.jpg` ~ `hero-30.jpg` — `새이미지/`로 받은 카투니 18장 + 리얼베이스 12장 원본 프레임 전부 사용
  - 원본은 `원본이미지/영상프레임_2026-07-13/`에도 그대로 보관 중
  - `realbase_v1_notext_3086.jpg`(→ hero-14.jpg)에는 "NetEase Games / 牵士之滨 INFINITE BORDERS" 로고가 화면에 박혀 있음. 처음엔 이것 때문에 제외했었는데, 사용자가 "그래도 다 넣어달라"고 확인해서 포함시킴 — 나중에 문제 되면 이 파일만 다른 프레임으로 교체하면 됨.
  - 예전 hero-01.png~05.png(얀기로/노르곤/오르곤/그린고르/쿠오코마 도감 일러스트)는 `원본이미지/hero-test-set/`에 보관 중.

## 나중에 소스 교체할 때 (영상/이미지 다시 받으면 여기부터)

### 영상 교체
`index.html` 안 `<script>` 태그 아래쪽, `facade-toon`/`facade-real` 클릭 이벤트에 유튜브 영상 ID가 하드코딩되어 있음:

```js
document.getElementById('facade-toon').addEventListener('click', (e) => {
  playVideo('toon', 'clMdal8VOGQ', document.getElementById('frame-toon'));
});
document.getElementById('facade-real').addEventListener('click', (e) => {
  playVideo('real', 'X_EfCIHTrwE', document.getElementById('frame-real'));
});
```

바꿀 것:
1. 위 두 줄의 유튜브 영상 ID 교체
2. 같은 파일 안 `<img src="https://img.youtube.com/vi/영상ID/hqdefault.jpg">` 두 곳(썸네일)도 새 영상 ID로 교체
3. 필요하면 `work-desc`(작업 설명 문구)도 새 영상 내용에 맞게 수정

### 히어로 배경 사진 교체
- 가장 쉬운 방법: `images/hero/hero-01.jpg` ~ `hero-10.jpg` 파일을 같은 이름으로 새 이미지로 덮어쓰기만 하면 코드 수정 없이 바로 반영됨.
- 사진 장수를 바꾸고 싶으면 `index.html`의 `<div class="hero-slideshow" id="slideshow">` 안 `.slide` div를 추가/삭제 (경로만 `images/hero/새파일명.jpg`으로 맞추면 됨).
- 새 영상/프레임을 줄 땐 `새이미지/` 폴더에 넣어주면 그걸 기준으로 골라서 작업함(로고/텍스트 박힌 프레임 있는지 미리 확인 후 제외함).
- 밝은 사진을 쓸 경우 `.slide.active{opacity:0.35}` 값을 조절해서 밝기 낮추는 게 좋음.

### 소개 문구/이름 등 텍스트 교체
`<div class="hero-sub">` 안 텍스트, `<h1 class="hero-name">` 안 이름을 직접 수정.

## 폴더 정리

- `원본이미지/` — 다 쓴 원본 소스와 작업 중 생긴 테스트 파일 모아둔 폴더. 사이트에는 안 쓰임, 보관용.
  - `원본이미지/hero-test-set/` — 예전 몬스터 도감 일러스트 5장(hero-01~05.png, 첫 테스트용)
  - `원본이미지/영상프레임_2026-07-13/` — 2026-07-13에 받은 릴 프레임 원본 30장(그중 10장만 골라 씀)
- `새이미지/` — 나중에 영상/이미지 새 소스 줄 때 여기에 넣어주면 인식하기 편함. 지금은 비어있음 — 다음 소스 받으면 여기 담고 작업 후 다시 `원본이미지/`로 정리함.
- `images/hero/` — 실제 사이트에 쓰이는 히어로 배경 슬라이드 이미지(`hero-01.jpg` ~ `hero-30.jpg`).

## GitHub 업데이트 방법 (git 없이 웹으로)

1. `https://github.com/J-balcon/J-balcon.github.io/upload/main/portfolio` 접속
2. 수정된 `index.html` (또는 이미지 파일)을 "choose your files"로 업로드
3. 같은 이름 파일이면 자동으로 덮어쓰기됨
4. 하단 "Commit changes" 클릭 → 커밋 완료
5. 이미지처럼 새 폴더 경로가 필요하면 URL 끝에 원하는 경로를 붙여서 접속하면 (예: `.../upload/main/portfolio/images/hero`) 그 경로로 업로드/생성됨
6. 배포 반영까지 캐시 때문에 1~2분 정도 걸릴 수 있음 — 안 바뀌어 보이면 잠시 후 새로고침

## 디자인 리뷰에서 나왔던 남은 항목 (보류 중)

- **CTA 버튼** ("이력서 다운로드" 또는 "쇼릴 전체보기") — 실제 이력서 PDF나 풀 릴 링크가 있어야 추가 가능. 나중에 파일 주면 추가하자.
- **포인트 컬러** — 지금은 흑백/실버 톤만 사용 중. 원하면 강조색 하나 추가 가능 (취향 문제라 보류해둠).

## 기술적으로 참고할 점

- 유튜브 임베드는 `youtube-nocookie.com` + `referrerpolicy="strict-origin-when-cross-origin"` 사용 중 (안 하면 임베드 153 에러 남).
- 히어로 텍스트가 화면 폭에 따라 다시 줄바꿈되지 않도록 `.hero-sub`의 `max-width`는 `min(92vw, 52rem)`로 고정해둠 — 문구를 더 길게 바꾸면 이 값도 같이 늘려야 할 수 있음.
- 이미지 슬라이드는 1600×900 캔버스에 일러스트를 하단 중앙 정렬로 배치한 구조라, 다른 비율의 사진을 넣을 땐 `.slide{background-size:cover}` 특성상 심하게 잘릴 수 있음 (필요하면 비슷한 방식으로 다시 가공해줄 수 있음).
