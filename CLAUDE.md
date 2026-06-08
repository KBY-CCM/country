# 이상형 월드컵 프로젝트

## 구조
- `index.html` — 단일 HTML 파일 (CSS/JS 인라인). 토너먼트 로직, UI 전부 포함.
- `titles.txt` — 첫 줄: `url.<slug>` (라우팅 슬러그), 이후 줄: `번호.후보제목` 목록.
- `images/` — 후보 이미지. 파일명은 번호 prefix로 매칭 (`1.png`, `2.jpg` 등).

## 배포 방식
- 로컬에서 작업 → GitHub Pages로 배포.
- URL 슬러그(`url.<slug>`)가 월드컵을 구분하는 키. 최종 URL은 `kby-ccm.github.io/<slug>/`.
- **월드컵 하나당 별도 레포** (`KBY-CCM/<slug>`). 기존 레포는 절대 건드리지 않는다.

## 새 월드컵 배포 절차 (안전 순서)
1. `titles.txt`의 첫 줄 `url.<slug>` 와 `0.<월드컵 제목>` 확인.
2. **푸시 전에 `git remote -v`로 origin 확인.** 다른 슬러그(예: 직전 월드컵)를 가리키고 있으면 그대로 `git push` 절대 금지.
3. `gh repo create KBY-CCM/<slug> --public --description "<설명>"` 으로 새 레포 생성.
4. 변경사항 커밋 후 직접 URL 푸시: `git push https://github.com/KBY-CCM/<slug>.git main`.
5. origin을 새 레포로 교체: `git remote set-url origin https://github.com/KBY-CCM/<slug>.git`. 이후 일반 `git push`가 안전해짐.
6. Pages 활성화: `gh api -X POST repos/KBY-CCM/<slug>/pages -f "source[branch]=main" -f "source[path]=/"`.

## 작업 규칙
- **새 월드컵 추가 시 기존 URL 슬러그/레포는 절대 삭제·덮어쓰지 않는다.** 배포된 기존 월드컵이 살아있어야 하므로.
- 이미지·텍스트 파일은 로컬에서 자유롭게 덮어써도 됨.
- 후보 목록은 `.txt` 파일 사용 (`.js` 래퍼 X).
- 파일명이 코드와 안 맞으면 코드(매니페스트/정규식)를 고친다. 사용자 파일을 일괄 rename하지 않는다.
- 이미지 파일명 형식: `<번호>.<설명>.<확장자>` (예: `1.사투리 해봐.png`). 매칭은 번호 prefix(`^\d+\.`) 기준이므로 설명 텍스트는 자유.

## 현재 배포 상태
- `country` — 지방인이 무조건 긁히는 순간 월드컵 (16강). https://kby-ccm.github.io/country/
- `goback` — 최악의 고백 월드컵 (이전). https://kby-ccm.github.io/goback/
- `ozon-style` — 최악의 오존 스타일링 월드컵. https://kby-ccm.github.io/ozon-style/
