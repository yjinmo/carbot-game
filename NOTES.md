# 카봇 숫자 대모험: 작업 메모

- 게임 파일: `index.html` (전체 HTML 문서). 아티팩트 링크: https://claude.ai/artifact/Q9BqcZFNkmVtmH7HjsqRLZ
  - 아티팩트로 올릴 때는 `index.html`에서 맨 앞 `<!doctype html>…<body>` 7줄과 맨 끝 `</body></html>`을 뺀 내용을 올린다. 같은 링크에 새 버전으로 올리려면 Artifact 도구에 `url`을 넘긴다.
- 실제 카봇 이미지: `PHOTOS`에 data: 주소(webp, 긴 변 400px, 하나에 10~18KB)로 들어 있다. 나무위키(i.namu.wiki)는 Cloudflare가 클라우드에서 막아(403) 네이버 이미지 검색 결과(장난감 상품 사진)에서 골랐다. 에이스·프론·스카이·댄디·스톰·펜타스톰 6개. 블랙 위저드는 쓸 만한 사진이 없어 `boss: []`로 두고 직접 그린 그림을 쓴다.
  - 사진 찾는 법: `https://search.naver.com/search.naver?where=image&query=...` HTML 안의 `"originalUrl"` JSON 조각에서 `viewerThumb`(search.pstatic.net) 주소를 내려받으면 된다. Bing 이미지 검색은 봇을 막는다.
- 아티팩트는 CSP 때문에 바깥 이미지를 막으므로 사진은 반드시 data: 주소로 넣는다.
- 이미지를 불러오지 못하면 `photoFail()`이 다음 후보로 넘어가고, 마지막에는 직접 그린 SVG(`carSide`, `robotDrawn`, `villainDrawn`)로 바뀐다.
- 보스전 펜타스톰은 사진 대신 만화풍 SVG(`pentaToon`)를 쓴다(사용자 요청). 필살기는 판마다 다르다(`SPECIALS`): 1판 펜타 무지개 빔, 2판 카봇 미사일 연발, 3판 천둥 번개 검. 공통 기 모으기 연출은 `finisher()`. 로봇 움직임: SVG를 `.t-legs/.t-upper/.t-arml/.t-armr/.t-head`로 나눠 CSS로 숨쉬기·눈 깜빡임, 연타 때 좌우 주먹(`punch-l/r`), 필살기 자세(`pose-beam/missile/sword`).
- 도로 주행 장면은 위에서 본 차 그림(`carTop`)을 그대로 쓴다.
- 테스트: Playwright로 처음부터 보스 승리까지 자동으로 플레이한다(문제 정답은 `state.items`에서 읽음).
