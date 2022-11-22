# React에서 API 호출하기 (axios, fetch)

> 서버와 데이터를 주고받기 위해서는 HTTP 통신을 해야 하는데,
> React에는 HTTP Client(HTTP 상에서 커뮤니케이션을 하는 자바 기반 컴포넌트) 내장 클래스가 존재하지 않는다.
>
> 따라서 React에서 \*AJAX(Asynchronous Javascript And XML)를 구현하려면
> JavaScript 내장객체인 XMLRequest를 사용하거나, 다른 HTTP Client를 사용해야 한다.
>
> - AJAX : 서버와 통신하기 위해 XMLHttpRequest 객체를 사용하는 것으로,
>   JSON, XML, HTML 그리고 일반 텍스트 형식 등을 포함한 다양한 포맷을 비동기로 주고받을 수 있다.
>
> HTTP Client 라이브러리에는 Fetch API, Axios가 있는데, 사용하는 형태에 약간 차이가 있다.

<br>

## 💡 fetch

> **자바스크립트 내장 라이브러리 (API 호출하는 역할)**
>
> 내장 라이브러리이기 때문에 별도의 모듈 설치가 필요하지 않은 장점이 있지만, 브라우저 호환성이 떨어지고 response timeout 처리 방법이 없는 등 기능적인 부분이 상대적으로 부족하다.

<br>

```jsx
fetch(url, options)
  .then((response) => console.log('response:', response))
  .catch((error) => console.log('error:', error));
```

- 첫번째 인자로 (API의) URL, 두번째 인자로 옵션 객체를 받는다.
  - 옵션(options) 객체에는 HTTP 방식(method), HTTP 요청 헤더(headers), HTTP 요청 전문(body) 등을 설정할 수 있다.
  - 응답(response) 객체로부터는 HTTP 응답 상태(status), HTTP 응답 헤더(headers), HTTP 응답 전문(body) 등을 읽어올 수 있다.
- fetch는 Promise 타입의 객체를 반환한다.
  - API호출이 성공했을 경우(then)에는 응답(response) 객체를 resolve 하고
  - 실패했을 경우(catch)에는 예외(error) 객체를 reject 한다.

<br>
<br>

## 💡 axios

> **node.js와 브라우저를 위한 http 통신 라이브러리**
>
> fetch처럼 promise를 지원한다는 공통점이 있지만, fetch와는 달리 브라우저 호환성이 좋고 편리하며 기능이 많다.
> 라이브러리 설치가 필요하다는 단점이 있지만 fetch에 비해 기능상으로 더 디테일하다는 큰 장점이 있다.

<br>

#### 🔖 axios 설치하기

```bash
# npm
npm install axios

# yarn
yarn add axios
```

- useInput 커스텀 훅 안에 useState, useCallback에 있는 로직을 미리 정의했기 때문에, 컴포넌트에서는 커스텀 훅을 사용하기만 하면 된다.

<br>

#### 🔖 axios 사용하기

> 1. 비동기로 서버에 요청을 보내고(request)
> 2. 서버로부터 응답이 오면(response) 제대로 응답이 왔을 때와 못 왔을 때를 구분하여 처리
>
> - 서버에 요청을 보냈을 때 응답이 오기까지 시간이 걸리므로 서버에 보내는 요청은 비동기 처리를 해주며, 그 이후에 응답을 바탕으로 처리하는 과정은 .then 이나 await를 이용한다.

- **서버에 요청을 보내는 axios의 request 메소드**

  - GET : 서버에서 어떤 데이터를 가져와서 보여줌
  - POST : 서버로 데이터를 보냄
  - PUT : 데이터베이스 내부 내용 갱신
  - DELETE : 데이터베이스 내부 내용 삭제

<br>

- **request 메소드를 사용하기 위해 전달해야 하는 정보들**

  1. 어떤 메소드를 사용할 것인지
  2. url 주소
  3. data (선택)
  4. params (선택)
     <br>

  ```jsx
  axios({
    //request
    method: 'get',
    url: 'url',
    responseType: 'type',
  }).then(function (response) {
    // response Action
  });
  ```

<br>

#### 🔖 GET

> axios.get(url[,config])

- 서버에서 데이터를 가져오는 GET 메소드는 두 가지 상황이 존재한다.
  <br>

  1. 지정된 단순 데이터 요청을 수행하는 경우 -> url만 파라미터로 넘김

     ```jsx
     async function getData() {
       try {
         //응답 성공
         const response = await axios.get('url주소');
         console.log(response);
       } catch (error) {
         //응답 실패
         console.error(error);
       }
     }
     ```

  2. 사용자 번호에 따라 다른 데이터를 불러오는 경우-> url과 함께 prams:{} 객체도 파라미터로 넘김
     ```jsx
     async function getData() {
       try {
         //응답 성공
         const response = await axios.get('url주소', {
           params: {
             //url 뒤에 붙는 param id값
             id: 12345,
           },
         });
         console.log(response);
       } catch (error) {
         //응답 실패
         console.error(error);
       }
     }
     ```

<br>

#### 🔖 POST

> axios.post(url, data[,config])

- 서버에 데이터를 보내는 POST 메소드에서는 데이터를 message body에 포함시켜 보낸다.
  보내는 방식은 GET 메소드에서 params를 보내는 것과 유사하다.

  ```jsx
  async function postData() {
    try {
      //응답 성공
      const response = await axios.post('url주소', {
        //보내고자 하는 데이터
        username: 'devstone',
        password: '12345',
      });
      console.log(response);
    } catch (error) {
      //응답 실패
      console.error(error);
    }
  }
  ```

<br>

#### 🔖 PUT

> axios.put(url,data[,config])

- DB의 내용을 수정하는 PUT 메소드는 서버 내부적으로 get -> post 하는 과정을 거치기 때문에 post 메소드와 비슷한 형식이다.

  ```jsx
  async function putData() {
    try {
      //응답 성공
      const response = await axios.put('url주소', {
        //항목에 새롭게 넣을 데이터
        username: 'stone',
        password: '123',
      });
      console.log(response);
    } catch (error) {
      //응답 실패
      console.error(error);
    }
  }
  ```

<br>

#### 🔖 DELETE

> axios.delete(url[,config])

- 데이터베이스 내부의 데이터를 삭제하는 DELETE 메소드는 일반적으로 body가 비어있는 형태
- query나 params가 많아서 헤더에 많은 정보를 담기 어려운 상황에 한해서만 두번째 인자에 data를 추가해준다.
  <br>

  1. 일반적인 delete

     ```jsx
     async function deleteData() {
       try {
         //응답 성공
         const response = await axios.delete('url주소');
         console.log(response);
       } catch (error) {
         //응답 실패
         console.error(error);
       }
     }
     ```

  2. 헤더에 정보가 많이 포함된 경우

     ```jsx
     async function deleteData() {
       try {
         //응답 성공
         const response = await axios.delete('url주소', {
           //헤더에 포함된 정보들
           data: {
             post_id: 1,
             comment_id: 13,
             username: 'foo',
           },
         });
         console.log(response);
       } catch (error) {
         //응답 실패
         console.error(error);
       }
     }
     ```

<br>
<br>

### 📚 Reference

&nbsp; https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8
&nbsp; https://axios-http.com/kr/docs/intro
&nbsp; https://yamoo9.github.io/axios/guide/
&nbsp; https://velog.io/@shin6403/React-axios%EB%9E%80-feat.-Fetch-API
&nbsp; https://www.daleseo.com/js-window-fetch/

<br>
<br>
