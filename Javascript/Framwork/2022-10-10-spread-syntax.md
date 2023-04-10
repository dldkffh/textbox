---
title: NextJS_Overview
authors: dldkffh
tags: [javascript, NextJS]
enableComments: false # for Gisqus
---

# **Next.js**

추천하는 강의 : [노마드 코더 - NextJS 시작하기](https://nomadcoders.co/nextjs-fundamentals)

<br/>

## **리액트 프레임 워크 종류**
 - Next.js : (아래 내용 참고)
 - Gatsby : 블로그할 때 좋음, HTML을 미리 만들어 시간벌고 그 사이 리액트로 로딩하는 거임. 그래프QL과 사용가능하면 추천
 - Remix : 서버 필요. 서버에서 랜더링. routes안에 위치해야 됨, 안전함 서버사이드에서 작동하니까. API URL, useState 필요 없음. 최근에 무료가 됨.

 *Express도 굳이 분류하자면 프레임워크다. 단지 프론트엔드 부분의 프레임워크가 아닐 뿐이다.*

<br/><br/>

[Next.js - React, Express.js 그리고 SSR을 한방에 - 생활코딩](https://www.youtube.com/watch?v=ECMB4kUCKWQ&list=PLb9-UFjdAdxuIpnm8qWb35cdBXAc_AkJ6&index=3)

## **Next.js 란?**
React + Express.js + React-Router-Dom + Server Side Rendering

> 기본적으로 Next.js에는 다음 시작 시 자체 서버가 포함됩니다.

*여기서는 Express가 서버라는데 공식문서에 자체서버라는 거 보니 그건 아닐 수 도 있을 것 같다. 그리고 Express, Hapi, Koa 세가지가 예제로 나오는데.. 이 세가지를 외부 서버로 사용할 수 있어 보인다.*

<br/>

## **주요 명령어**
```powershell
npm run dev  //개발환경실행
npm run build  //배포 파일 생성
npm run start  //서비스 시작
```

`npm run build`를 하면 `.next`폴더에 빌드용 파일이 생성된다. 그후에 `npm run start`를 하면 실사용 서버가 실행된다.  

빌드한 후 `.next`, `package.json` 이걸 두 파일만 가지고 `yarn`, `yarn start`해도 실행이 됐음  
솔직히 이게 정석인지 모르겠는데 몇번 더 실험해볼 필요는 있어보임

<br/>

## **시작**
```powershell
yarn create next-app
yarn add next react react-dom
```

<br/>

## **네임드 파일 이름**
```js
/pages/_document.js  //<head> 태그 안에 작성될 CDN이나 공통으로 추가될 meta태그를 작성
/pages/_app.js  //공통되는 레이아웃을 작성
/pages/_error.js  //에러 페이지에서 공통으로 사용
/next.config.js  //웹팩 플러그인과 Nextjs 라우팅 설정을 작성, 리다이렉트 설정 가능
```

<br/>

## **Route**

*라우터는 가히 혁명적인 수준이다.*

/pages/index.js -> http://a.com/  
/pages/sub/index.js -> http://a.com/sub/  
/pages/sub/about.js -> http://a.com/sub/about  
/pages/sub/[id].js -> http://a.com/sub/1 , http://a.com/sub/2  
/pages/sub/_app.js : 이런건 url로 못 들어감  

`/pages/`안에 만드는 애들은 리액트 문법을 따라야함  
`useRouter`를 이용하면 라우트된 id값을 가져올 수 있음

<br/>

## **API Route**
/pages/api/index.js -> http://a.com/api  
/pages/api/[id].js -> http://a.com/api/:id  


<br/>

## **환경변수**
`/.env`  
API_URL  
NEXT_PUBLIC_API_URL : 외부에 노출되는 API  

환경변수로 선언을 해놓으면
```
DB_HOST=localhost
DB_USER=myuser
DB_PASS=mypassword
```

```javascript
// pages/index.js
export async function getStaticProps() {
  const db = await myDB.connect({
    host: process.env.DB_HOST,
    username: process.env.DB_USER,
    password: process.env.DB_PASS,
  })
  // ...
}
```
`process.env.[환경변수]` 형태로 불러오는게 가능

<br/>


## **getServerSideProps()**
page에서 서버 측 랜더링 함수인 `getServerSideProps()`함수를 export하는 경우, Next.js는 `getServerSideProps()`에서 반환된 데이터를 사용하여 각 request에서 이 페이지를 pre-render합니다. `getServerSideProps()`는 서버 측에서만 실행되며 브라우저에서는 실행되지 않습니다.

```javascript
export default function Home({ results }) {
  return (
    <div>
      {result?.map((movie) => (
        <div key={movie.id}>
          <h4>{movie.original_title}</h4>
        </div>
      ))
      }
    </div>

    <style jsx>{`
      ...
    `}</style>
  );
}

export async function getServerSideProps() { //백엔드 처리 부분, 유저에게는 안보임
  const { result } = await (
    await fetch(`[api_link]`)).json();
    return {
      props: {
        results,
      }
    };
}
```

<br/><br/>  

## **Style**
이전처럼 `sass` + `styled-components` + `styled-jsx` 이 스택으로 쓸거임   
기존에 사용하던 sass, styled-components, styled-jsx를 모두 기본적으로 제공(?) 하는 것 같다. 테스트를 해봐야겠지만 아마 다른 인스톨 없이 기본적으로 제공하는 것으로 보임.


## **Image Optimization**
```javascript
import Image from 'next/image'

export default function Home() {
  return (
    <>
      <h1>My Homepage</h1>
      <Image
        src="/me.png" //public에 두면 알아서 가져옴
        alt="Picture of the author"
        width={500}
        height={500}
      />
      <p>Welcome to my homepage!</p>
    </>
  )
}
```

<br/><br/>

[**Fullstack Example with Next.js (REST API)**](https://github.com/prisma/prisma-examples/tree/latest/javascript/rest-nextjs)  
[prisma - quickstart](https://www.prisma.io/docs/getting-started/quickstart)  
[Next.js + MySQL](https://github.com/vercel/next.js/tree/canary/examples/with-mysql)  

## **API**

개인적으로 생각한건  
`mysql` + `prisma` + `nextjs-rest-api-routes`  

[RBAC와 ABAC 의 특징 비교: 정의 및 사용 사례](https://www.okta.com/kr/identity-101/role-based-access-control-vs-attribute-based-access-control/)

### **RBAC vs. ABAC**

- RBAC(Role-Based Access Control)란?
  RBAC 프로토콜에서는 이 사람의 역할에 따라 결정
  균일적, 게층적, 제한적, 대칭적

- ABAC(Attribute-Based Access Control)란? 
  사용자, 리소스속성, 환경에 따라 결정

규모가 작을 수록 규칙을 적을 수록 RBAC가 편하다

<br/>

## Prisma
NextJS를 설치하면 prisma를 쓸수 있다.

```powershelld
yarn add @prisma/client
npx prisma generate
```
하지만 client는 따로 다운 받아야 한다.  
generate도 해줘야 client가 제대로 돌아간다.

<br/>

`.env`에 `DATABASE_URL`를 추가하고
```ini
DATABASE_URL=mysql://<USERNAME>:<PLAIN_TEXT_PASSWORD>@<ACCESS_HOST_URL>/<DATABASE_NAME>
```

```powershell
npx prisma init
```
위 명령어를 입력하자.

프로젝트에 `/prisma/`폴더와 그안에 `schema.prisma`파일이 생길 것이다.

```powershell
npx prisma db pull
```
해당 명령어로 이미 생성된 db와 연결 가능!

<br/>

<br/>


[NextAuth.js Example App](https://github.com/nextauthjs/next-auth-example)
## [NextAuth.js](https://next-auth.js.org/)
```powershell
yarn add next-auth @prisma/client @next-auth/prisma-adapter
yarn add prisma --dev
```

[NextAuth Email](https://next-auth.js.org/providers/email) - 이건 이메일 인증이라 아님
  
[NextAuth Credentials](https://next-auth.js.org/configuration/providers/credentials)  
[NextAuth Callbacks](https://next-auth.js.org/configuration/callbacks)  
[NextAuth Models](https://next-auth.js.org/adapters/models)  
  
[next-auth/jwt](https://next-auth.js.org/getting-started/upgrade-v4#next-authjwt)  


<br/>

[SuperTokens Example](https://github.com/vercel/next.js/tree/canary/examples/with-supertokens)
## [SuperTokens](https://supertokens.com/docs/guides)

```powershell
yarn add supertokens-auth-react
yarn add supertokens-node
```

<br/><br/>

### Quest

- 여태 배운 것을 사용하여 회원가입/회원관리 구현하기

- CKeditor를 사용해 기본 게시판을 만들어 보자


<br/><br/>  

---

## 참고

[Introduction | Learn Next.js (nextjs.org)](https://nextjs.org/docs/getting-started)  
[NextJS MySQL example. Get MySQL data into a react app using Node JS](https://www.youtube.com/watch?v=aprLiG34b50)

---

<br/><br/>

## **궁금증 - 짤팁**

> powershell에서 `code [filename or path]`를 하면 VScode가 실행된다.  

<br/>

### **자바스크립트 코드 안보이게 할 수 없나? : Build방법**
> 리액트의 경우에도 `npm run build`후 `build`파일과 `package.json`두개만 가지고 빌드하라고 나온다. 단, `/.env`안에 `GENERATE_SOURCEMAP=false`를 추가해야 소스가 개발자 도구로 봐도 안보인다!
```powershell
 File sizes after gzip:

  220.74 kB  build\static\js\main.a20e1c87.js
  35.73 kB   build\static\css\main.37263ea4.css
  1.78 kB    build\static\js\787.b03576d6.chunk.js

The project was built assuming it is hosted at /.
You can control this with the homepage field in your package.json.

The build folder is ready to be deployed.
You may serve it with a static server:

  npm install -g serve
  serve -s build

Find out more about deployment here:

  https://cra.link/deployment
  
```

> 프론트엔드 안에서 실행되는 걸 hydration이라고 부른다.

### **Fetch란?**
fetch 매서드는 JavaScript에서 서버로 네트워크 요청을 보내고 응답을 받을 수 있도록 해주는 매서드이다. api를 불러오고, 정보를 내보내주느 함수.   
method 
- GET
- POST
- PUT
- DELETE
- ...

### **API란?**
데이터와 데이터베이스에 대한 출입구, 모든 접속의 표준화.  
기계 및 운영체제 등 과 상관없이 모든 접속을 표준화 시켜 액세스를 얻을 수 있게 한다.  
범용 플러그와 같이 작용

<br/>

### **NGINX란?** 
HTTP와 리버스 프록시, IMAP/POP3 등의 서버 구동이 가능한 가벼우면서도 강력한 프로그램을 목표로 개발된 오픈 소스 웹 서버 프로그램  
리눅스 기반으로 구축하는 웹 서버의 경우, 기존의 LAMP(Linux + Apache + MySQL/MariaDB + PHP/Python/Perl)에서 Apache 대신 (E)NGINX로 대체된 LEMP를 쓴다.  
Node.js 서버에 NGINX를 프록시 서버로 사용하면 안전하다.
> "You just may be hacked when some yet-unknown buffer overflow is discovered. Not that that couldn't happen behind nginx, but somehow having a proxy in front makes me happy"  - Ryan Dahl  
> "아직 알려지지 않은 버퍼 오버플로가 발견되면 해킹을 당할 수 있습니다. nginx 뒤에서는 일어날 수 없는 일이 아니지만 앞에 프록시가 있다는 것은 저를 기쁘게 합니다."  

*NGINX로는 웹서버와 리버스 프록시(, 로드 발란서, 메일 프록시, HTTP 캐시서버)를 만들 때 쓰고, Express는 웹프레임워크로 웹서버 만들때 쓴다. 간단하게 만들때는 Express를 쓰고 고성능 서버를 만들때에는 NGINX를 선호하게 된다.*

<br/>

### **프록시서버란?** 
클라이언트가 자신을 통해서 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해 주는 컴퓨터 시스템이나 응용 프로그램을 가리킨다. 서버와 클라이언트 사이에 중계기로서 대리로 통신을 수행하는 것을 가리켜 '프록시', 그 중계 기능을 하는 것을 프록시 서버라고 부른다.
- 포워드 프록시(forward proxy)는 인터넷 상에서 어디로든지 리퀘스트를 전송해주는 프록시이다.
- 리버스 프록시(reverse proxy)는 인터넷에서 리퀘스트를 받으면, 내부망 내의 서버로 전송해준다.

*근데 굳이 리버스 프록시를 두냐 개발 규모 좀 고려해라.... 여기가 트위터냐? 그냥 홈페이지 잖아*  
[Tumblr가 가진 기술과 개발 문화](https://www.mimul.com/blog/tumblr-architecture-and-culture/)

<br/>

### **그럼? 레디스는? 그것도 프록시 서버가 아닌가?**
레디스는 Remote Dictionary Server의 약자로서, "키-값" 구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 비관계형 데이터베이스 관리 시스템이다.  
레디스는 모든 데이터를 메모리에 저장하고 조회합니다. 즉, 인메모리 데이터베이스 입니다.
프록시 서버가 아니다.

### **CRUD VS. API**
*일단 비교하는 영역은 아닌듯하다. NextJS에서 CRUD 기본은 어느정도 제공하는 듯  
다만 문제가 있다면, API를 결국 미래에 하긴 해야 할듯 하다라는 것*  
*JDBC도 JAVA API임*

**CRUD**는 DB SQL용어임  
Create(생성), Read(조회/읽기), Update(갱신/수정), Delete(삭제)

[API란 무엇인가요?](https://aws.amazon.com/ko/what-is/api/)  
**API**는 그게 아님 인터페이스임  
API는 정의 및 프로토콜 집합을 사용하여,  
두 소프트웨어 구성 요소가 서로 통신할 수 있게 하는 메커니즘.  
API는 Application Programming **Interface**(애플리케이션 프로그램 인터페이스)의 줄임말  

<종류>
- SOAP API : 단순 객체 접근 프로토콜, 클라이언트와 서버는 XML을 사용하여 메시지를 교환
- RPC API : API를 원격 프로시저 호출, 클라이언트가 서버에서 함수나 프로시저를 완료하면 서버가 출력을 클라이언트로 다시 전송
- Websocket API : JSON 객체를 사용하여 데이터를 전달하는 또 다른 최신 웹 API, 양방향 통신을 지원, 서버가 연결된 클라이언트에 콜백 메시지를 전송할 수 있어 REST API보다 효율적
- REST API : 오늘날 웹에서 볼 수 있는 가장 많이 사용되고 유연한 API, 클라이언트가 서버에 요청을 데이터로 전송

<유형>  
프라이빗 API, 퍼블릭 API, 파트너 API, 복합 API 

API 엔드포인트는 API 통신 시스템의 최종 접점  
보안과 성능이 중요함
-> 보안은 인증토큰과 API키로 보호한다.

### **GraphQL**
GraphQL은 API용으로 특별히 개발된 쿼리 언어로서, 클라이언트에게 요청한 데이터만 제공하는 것을 우선으로 합니다. 또한 API를 빠르고 유연하며 개발자 친화적으로 만들도록 설계되었습니다. REST의 대안으로서 GraphQL은 프런트엔드 개발자에게 단일 GraphQL 엔드포인트로 여러 데이터베이스, 마이크로서비스 및, API를 쿼리할 수 있는 기능을 제공합니다.

### **멱등성**
동일한 요청을 한 번 보내는 것과 여러 번 연속으로 보내는 것이 같은 효과를 지니고, 서버의 상태도 동일하게 남을 때, 해당 HTTP 메서드가 멱등성을 가졌다고 말합니다. 다른 말로는, **멱등성 메서드에는 통계 기록 등을 제외하면 어떠한 부수 효과(side effect)도 존재해서는 안됩니다.** 올바르게 구현한 경우 `GET`, `HEAD`, `PUT`, `DELETE` 메서드는 멱등성을 가지며, `POST` 메서드는 그렇지 않습니다.

<br/>

### [Nodemailer](https://www.npmjs.com/package/nodemailer)
Send emails from Node.js – easy as cake!

### [Naver cloud - Simple & Easy Notification Service](https://www.ncloud.com/product/applicationService/sens)
알람 및 메시지 전송 기능을 쉽게 구현할 수 있는 서비스 제공  
Simple & Easy Notification Service를 통해 서비스에 메시지 및 알람 전송 기능을 간편하게 구현할 수 있습니다. 메시지 전송 현황을 실시간으로 확인하고, 전송 이력을 특정 기간 별로 조회할 수 있어 효율적인 서비스 운영이 가능합니다.

### Style 참고 할만한 사이트
- [dribbble](https://dribbble.com/)  

- [CoreUI Free Template](https://github.com/coreui/coreui-free-bootstrap-admin-template#installation)  
- [**coreui-free-react-admin-template**](https://github.com/coreui/coreui-free-react-admin-template)  
- [Redux Toolkit TypeScript Example](https://github.com/vercel/next.js/tree/canary/examples/with-redux) : CoreUI 사용시 필요  
```powershell
npm install @coreui/react
npm install @coreui/coreui
```  
  
### **async function**
자바스크립트 비동기 함수
비동기 함수는 `async`키워드로 선언된 함수이며 그 `await`안에 키워드가 허용됩니다.  
`await`사용하면 약속 체인을 명시적으로 구성할 필요 없이 비동기식 약속 기반 동작을 보다 깔끔한 스타일로 작성할 수 있습니다.  