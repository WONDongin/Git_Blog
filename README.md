## 블로그 작성
1. 글은 blog 폴더에 작성하며, `[date]_[title]_[category]_[thumnail]_[description].md` 형식으로 작성합니다.
2. 썸네일을 사용하지 않는 경우, `[date]_[title]_[category]_[].md` 형식으로 작성합니다.
3. 썸네일의 경로는 img 폴더에서 관리하거나 퍼블리싱 된 이미지 링크를 사용할 수 있습니다.
4. `data/localBlogList.json`을 수정하여 화면에 출력할 글을 관리합니다.

## 메뉴 관리
우측 상단의 메뉴를 관리하는 방법은 다음과 같습니다.
1. menu 폴더에 `사용하고싶은 메뉴 이름.md` 형식으로 저장하면 메뉴로 생성됩니다.
2. `data/local_blogMenu.json`을 관리하여 화면에 출력할 메뉴를 관리합니다.


## 디자인 수정
- `style/globalStyle.js` 파일을 수정하여 전체적인 스타일을 수정할 수 있습니다.
- Tailwind CSS를 이용하여 손쉽게 나만의 스타일을 적용할 수 있습니다.
- 프로필로 사용할 수 있는 위니브 프렌즈의 이미지와 썸네일 일러스트를 제공합니다.


## 폴더 트리

  | 폴더명 | 파일명               | 함수                                   | 변수                                         | 비고                          |
  | ------ | -------------------- | -------------------------------------- | -------------------------------------------- | ----------------------------- |
  | style  | globalStyle.js       |                                        |                                              | 전역 스타일 설정              |
  | style  | blogContentsStyle.js |                                        |                                              | 블로그 컨텐츠 스타일 설정     |
  | JS     | config.js            |                                        | siteConfig                                   | 사이트 설정 정보              |
  | JS     | URLparsing.js        | extractFromUrl()                       | url(url obj), pathParts(쿼리스트링), isLocal | URL 파싱, 스키마 확인         |
  | JS     | render.js            | renderBlogPosts(), renderMenu()        |                                              | 데이터를 DOM에 렌더링         |
  | JS     | initData.js          | initDataBlogList(), initDataBlogMenu() | blogList, blogMenu                           | 초기 데이터 로딩, 스키마 확인 |
