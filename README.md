# 유진호 포트폴리오

Hugo와 Enervoid 테마로 만든 원페이지 포트폴리오입니다. About에서 관심 분야와 학습 목표를, Projects에서 Roblox와 Unity 프로젝트의 제작 과정 및 플레이 영상을 볼 수 있습니다. Contact에는 연락 수단을 정리했습니다.

- [공개 사이트](https://jhhj5044-cloud.github.io/myprofile/)
- [GitHub 저장소](https://github.com/jhhj5044-cloud/myprofile)
- [GitHub Actions 배포 이력](https://github.com/jhhj5044-cloud/myprofile/actions)

## 개발 환경과 설치

1. 운영체제에 맞는 [Git 설치 프로그램](https://git-scm.com/install/)을 설치합니다.
2. [Hugo v0.167.0 릴리스](https://github.com/gohugoio/hugo/releases/tag/v0.167.0)에서 운영체제와 CPU에 맞는 **Extended** 압축 파일을 받습니다. Windows에서는 압축을 풀고 `hugo.exe`가 있는 폴더를 사용자 환경 변수 `Path`에 추가한 뒤 터미널을 다시 엽니다.
3. 아래 명령으로 설치를 확인합니다. Hugo 출력에 `v0.167.0`과 `extended`가 표시되어야 합니다.

```sh
git --version
hugo version
```

테마는 `site/themes/template/`에 포함되어 있습니다. 로컬 미리보기와 기본 빌드에는 별도의 테마 설치나 npm 설치가 필요하지 않습니다. 배포 워크플로에서 사용하는 Python, Node.js, Go, Dart Sass는 GitHub Actions에서 설치합니다. 브라우저에서 외부 CDN의 스타일과 아이콘을 불러오려면 인터넷 연결이 필요합니다.

## 로컬 실행과 빌드

저장소를 복제한 뒤 아래 명령을 저장소 루트에서 실행합니다.

```sh
git clone https://github.com/jhhj5044-cloud/myprofile.git
cd myprofile
hugo server --source site --config hugo.toml,pages.json --baseURL http://localhost:1313/myprofile/ --port 1313
```

[로컬 미리보기](http://localhost:1313/myprofile/)에서 화면을 확인합니다. 서버를 종료하려면 터미널에서 **Ctrl+C**를 누릅니다.

배포 주소를 기준으로 정적 파일을 생성하려면 같은 위치에서 다음 명령을 실행합니다.

```sh
hugo --source site --config hugo.toml,pages.json --environment production --destination ../public
```

빌드 결과는 저장소 루트의 `public/`에 생성됩니다. `site/hugo.toml`과 `site/pages.json`을 함께 읽으며, Pages의 운영 주소는 `site/pages.json`에 있습니다.

## 콘텐츠 수정 위치

| 수정 대상 | 파일 또는 폴더 |
|---|---|
| About 소개, 관심 분야, 기술과 경험, 목표 | [site/content/about.md](site/content/about.md) |
| Roblox 상세 내용, 카드 정보, 개발 기간과 상태 | [site/content/projects/forge.md](site/content/projects/forge.md) |
| Unity 제목, 기술 목록, 카드 정보, 영상 경로 | [site/content/projects/pxl.md](site/content/projects/pxl.md) |
| Unity 소개·제작 과정·회고의 본문과 배치 | [unity-project.html](site/themes/template/layouts/_partials/unity-project.html) |
| 홈과 Contact | [home.html](site/themes/template/layouts/home.html) |
| 메뉴와 사이트 기본 설정 | [site/hugo.toml](site/hugo.toml) |
| 프로젝트 이미지 및 영상 | [site/static/images/projects/](site/static/images/projects/) · [site/static/videos/projects/](site/static/videos/projects/) |

새 미디어를 추가할 때는 파일도 Git으로 추적합니다. 콘텐츠 설정에서 정적 파일을 참조할 때는 `images/projects/파일명.png`처럼 앞에 슬래시를 붙이지 않습니다. 템플릿의 Hugo `relURL`이 공개 사이트의 `/myprofile/` 경로를 반영합니다.

## 커밋과 GitHub Pages 재배포

1. 로컬에서 화면과 링크를 확인한 뒤 변경한 소스 파일을 커밋합니다. 다음은 About을 수정했을 때의 예입니다.

```sh
git status
git diff -- site/content/about.md
git add -- site/content/about.md
git commit -m "About 소개 수정"
git push origin main
```

2. GitHub 저장소의 **Settings → Pages → Build and deployment → Source**가 **GitHub Actions**인지 확인합니다.
3. `main`에 푸시하면 [hugo-pages.yml](.github/workflows/hugo-pages.yml)이 자동 실행됩니다. 워크플로는 [빌드 스크립트](.github/pages_build.py)로 사이트를 빌드하고 `public/` 결과물을 Pages에 배포합니다.
4. [Actions](https://github.com/jhhj5044-cloud/myprofile/actions)에서 해당 커밋의 빌드와 배포가 성공했는지 확인한 뒤, [공개 사이트](https://jhhj5044-cloud.github.io/myprofile/)에서 변경된 페이지를 열어 확인합니다.

## 출처와 이용 조건

- **Enervoid 테마** — [Enerhim/enervoid-theme](https://github.com/Enerhim/enervoid-theme), Himanshu Sharma, MIT License. 테마를 포트폴리오에 맞게 수정했으며 [저작권 고지와 라이선스 전문](LICENSE)을 보존합니다.
- **프로젝트 기록** — Roblox·Unity 프로젝트의 편집 화면, 플레이 화면과 영상은 제작 결과를 보여주는 캡처입니다. Roblox 프로젝트 개발 과정에는 생성형 AI를 활용했습니다.
- **프로필 이미지** — [Lorem Picsum](https://picsum.photos/)의 동적 이미지를 `site/hugo.toml`에서 불러옵니다. 특정 사진의 원작자와 개별 이용 조건은 확인하지 않았습니다.

| 외부 자료 | 사용 위치와 이미지 출처 |
|---|---|
| [Superfighters 스크린샷](site/static/images/projects/superfighters.png) | Roblox 상세 페이지의 제작 동기 · [네이버 블로그 게시글](https://m.blog.naver.com/gilja0525/221735310113) |
| [Vampire Survivors 스크린샷](site/static/images/projects/vampire-survivors.jpg) | Unity 상세 페이지의 프로젝트 소개 · [Vampire Survivors Steam 상점 페이지](https://store.steampowered.com/app/1794680/Vampire_Survivors/) |

외부 이미지와 게임 자산에는 테마의 MIT 라이선스가 적용된다고 가정하지 않으며, 재사용하려면 해당 자료의 출처와 이용 조건을 따로 확인해야 합니다.
