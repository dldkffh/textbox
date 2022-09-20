## npm 명령어
npm을 사용하기 위해서는 몇가지 명령어를 알아둘 필요가 있는데, 프론트엔드 개발을 위해서 사용하는 npm 명령어는 대표적으로 아래와 같다.

```powershell
npm init // package.json 생성
npm install // package.json 파일 및 해당 종속성에 나열된 모든 모듈을 설치
npm install package_name@버전 // 특정 패키지의 특정 버전 설치
npm install 주소 // 특정 저장소 내 패키지 설치. 주로 github을 이와 같이 설치합니다.
npm install package_name -g // 옵션. 글로벌로 설치. 로컬의 다른 프로젝트도 이 패키지를 사용 가능하게 됩니다.
npm uninstall // 패키지 삭제 명령어입니다.
npm update // 설치한 패키지들을 업데이트해줍니다.
npm dedupe // 중복 설치된 패키지들을 정리해주는 명령어입니다.
```