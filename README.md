# 김철수 포트폴리오

종이·먹 2톤 "스크랩북" 디자인의 원페이지 포트폴리오. 빌드 도구 없이 `index.html` 한 파일로 동작하는 정적 사이트입니다.

## 구성
```
index.html   # 마크업 + CSS(디자인 토큰은 <style> 상단 :root) + 바닐라 JS
vercel.json  # 정적 배포 설정(클린 URL, 보안 헤더)
```
- 이미지 0장: 종이 질감·찢어진 가장자리·손그림은 전부 CSS/SVG 코드
- 외부 의존성: Google Fonts만 사용 (Instrument Serif, Nanum Myeongjo, Manrope, Noto Sans KR, Gochi Hand, Nanum Pen Script)
- `prefers-reduced-motion` 설정 시 모든 모션 해제

## 로컬 미리보기
```bash
npx serve .      # 또는 python3 -m http.server 3000
```

## GitHub → Vercel 배포
1. GitHub에서 새 저장소 생성(예: `portfolio`) 후 이 폴더를 push
   ```bash
   git init && git add . && git commit -m "init portfolio"
   git branch -M main
   git remote add origin https://github.com/<계정>/portfolio.git
   git push -u origin main
   ```
2. vercel.com → **Add New… → Project** → 해당 저장소 Import
3. Framework Preset: **Other**, Build Command 비움, Output Directory 비움(루트) → **Deploy**
4. 이후 `main`에 push할 때마다 자동 재배포, PR마다 프리뷰 URL 생성
5. 커스텀 도메인: Project → Settings → Domains 에서 `www.chulsoo-policy.com` 추가 후 DNS에 CNAME `cname.vercel-dns.com` 등록

## 수정 지점
| 바꿀 것 | 위치 |
|---|---|
| 색·폰트·크기 | `<style>` 상단 `:root` 토큰 |
| 프로필 사진 | `.photo` 안의 `.photo__mono`/`.photo__hint`를 `<img src="profile.jpg" alt="김철수" style="width:100%;height:100%;object-fit:cover">`로 교체하고 이미지 파일을 같은 폴더에 추가 |
| 경력·학력·역량 문구 | 각 `<section id="experience|education|skills">` |
| 공유 미리보기 이미지 | `<head>`에 `<meta property="og:image" content="https://도메인/og.png">` 추가 |

## 나중에 Next.js로 옮길 때
첨부 레퍼런스(paper-funnel)와 같은 구조로 섹션을 `components/sections/*.tsx`로 쪼개고, `<style>`을 `app/globals.css`로, 스크롤 로직은 Motion(`useScroll`, `whileInView`)으로 대체하면 됩니다. 클래스명은 레퍼런스와 맞춰 두었습니다.
