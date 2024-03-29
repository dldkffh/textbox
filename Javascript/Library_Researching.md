<!-- prettier-ignore -->
<br />

## 필요해 보이는 컴포넌트 찾기

### 겉
1. Bootstrap5 : 기본 구조
2. react-icons : 아이콘

3. react-date-range : 달력

### 속
1. react-router-dom : 구조
2. redux : state control
3. axios : post 통신

### 기타
- CSS : SCSS(sass)
- react-hook-form : 회원 가입 또는 양식 입력시
- 주소 API : https://postcode.map.daum.net/guide 

<br />

## 일단 사용되는 package 확인 좀....

<br />

비슷한 용도로 쓰이는 라이브러리들이 꽤 됨

1. **Redux** : 상태 관리 라이브러리는 Recoil, Redux가 유명한데 여기서는 **_Redux_**를 쓸듯  
https://ko.redux.js.org/introduction/installation/

2. **react-dom** : 이건 react 기본

2. **react-router-dom** : 이건 따로 설치해아함 Redux랑 이것이 날 그냥 어지럽게 해...

3. fontawesome : 아이콘 옵션 솔직히 그냥 **react-icon**으로 대체 해도 될듯 솔직히 왠만한 프로젝트는 **react-icon**로 다 커버 가능할듯
4. **reactstrap** : react-bootstrap대신에 적용해도 될만한 건가? 사용 방법만 좀 다른 듯
   https://www.geeksforgeeks.org/difference-between-reactstrap-and-react-bootstrap/  
   일단 예시에는 부트스트랩4를 사용해서 ClassName이 엄청 길고 어떤건 그냥 reactstrap Hook으로 처리함... Class가 너무 많으면 여러 개발자가 구분하기 어려워서 그렇다는데 그건 hook도 마찬가지 아닌가... 여러 사람이 만들었나?

```sh
npm install reactstrap react react-dom
```

reactstrap은

```js
<Nav style={{ backgroundColor: "#f1f1f1" }}>Something</Nav>
```

또는

```js
import styles from "./Component.module.css";
<Nav className={styles.Component}>Something</Nav>;
```

```css
Component {
  background-color: #f1f1f1;
}
```

이런식으로 색을 정해야 한다고함 흠...  
그냥 bootstrap 쓸까? ㅋㅋㅋㅋㅋㅋㅋ reactstrap에 scss 추가해도 될것 같기함

5. **apexcharts** : 이번 과제에서 가장 적합한 차트가 아닌가 더 뭐 필요하면 d3.js나 victory.js?
6. **rc-slider** : 슬라이더 필요하게 될 수도 있음
7. **react-date-range** : 전에 사장님이 보여줬던 데모에도 이거 쓰던데... 찾았다 이거다 그냥 이거 써! 캘린더도 있고 다있다음

8. **sass** : less, node-sass도 있지만 역시 sass가 깔쌈하게 제일 나은 듯 이슈도 적고. less는 문법이 sass보다 덜 직관적이고 sass-node는 node버전에 종속이 되서 나중가면 관리하기 불편할 듯
   https://npmcompare.com/compare/less,node-sass,sass

9. nvs : nvm, nvm-windows도 있다고함 현재 PC 자체에 설치된 버전을 깔면 path오류남 그게 아니여도 path 오류 그냥 나는 듯;;;

```sh
choco install nvs
```

10. ***axios*** : 이걸 이용해서 jwt 방식으로 소통한다는 건가?  
axios.post 그거 쓸려구 쓰는 거 아닌가? 아닌가? 아닌가? 일단 그렇다고 생각하자  
https://jwt.io/  
https://velog.io/@yaytomato/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%90%EC%84%9C-%EC%95%88%EC%A0%84%ED%95%98%EA%B2%8C-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EC%B2%98%EB%A6%AC%ED%95%98%EA%B8%B0  



<br /><br /><br />

## 기타 react 관련 정리

1. ### import

```js
import 객체, {객체} from [위치]
```

여기서 {}는 변수를 보내주는 방식의 차이  
{}는 export한 값을 가져올 때 사용
<br />

2. ### export

```javascript
export { 객체 };
```

<br />

3. React Router Tutorial  
   https://www.youtube.com/watch?v=Law7wfdg_ls
<br /><br />

### React Dom 개념이 부족하다면???
<br />

1. MDN Web Docs - React 시작하기(추천)  
   https://developer.mozilla.org/ko/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started  
   친절한 설명!

2. 리액트 ReactDom Docs(추천)  
   https://reactjs.org/docs/react-dom.html  
   https://reactrouter.com/

3. ***import { someting } from react***로 가져올 수 있는 거 (possible exports)
    Children, Component, Fragment, Profiler, PureComponent, StrictMode, Suspense, __SECRET_INTERNALS_DO_NOT_USE_OR_YOU_WILL_BE_FIRED, cloneElement, createContext, createElement, createFactory, createRef, forwardRef, isValidElement, lazy, memo, useCallback, useContext, useDebugValue, useEffect, useImperativeHandle, useLayoutEffect, useMemo, useReducer, useRef, useState, version

4.  ***import { someting } from react-router-dom*** possible exports  
   BrowserRouter, HashRouter, Link, MemoryRouter, NavLink, Navigate, Outlet, Route, Router, Routes, UNSAFE_LocationContext, UNSAFE_NavigationContext, UNSAFE_RouteContext, createRoutesFromChildren, createSearchParams, generatePath, matchPath, matchRoutes, renderMatches, resolvePath, unstable_HistoryRouter, useHref, useInRouterContext, useLinkClickHandler, useLocation, useMatch, useNavigate, useNavigationType, useOutlet, useOutletContext, useParams, useResolvedPath, useRoutes, useSearchParams


<br /> <br /><br />

## 짤팁
- prittier은 'format on Save'하라는데 그거 그냥 끄고, 'Default Formatter' 이걸 'prettier - code formatter'로 하고 그냥 '바로 가기 키'에 설정해 놓는게 맘편함

### 평소에 자주쓰는 키
- ctrl + alt + b : prettier
- ctrl + alt + m : minify
- ctrl + alt + n : run code
- ctrl + alt + s : stop run code




