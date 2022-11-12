# HTTP Request Method

> HTTP 메소드는 클라이언트가 하고 싶은 처리를 서버에게 전하는 역할을 한다.
> 메소드 종류 총 8개가 존재하며 아래와 같다.

<br>

## 💡 HTTP Request Method 종류

> 1. GET: 서버로 부터 데이터를 취득
> 2. POST: 서버에 데이터를 추가, 작성 등
> 3. PUT: 서버의 데이터를 갱신, 작성 등
> 4. DELETE: 서버의 데이터를 삭제
> 5. HEAD: 서버 리소스의 헤더(메타 데이터의 취득)
> 6. OPTIONS: 리소스가 지원하고 있는 메소드의 취득
> 7. PATCH: 리소스의 일부분을 수정
> 8. CONNECT: 프록시 동작의 터널 접속을 변경

<br>
<br>

## 💡 CRUD

> CRUD란 'Create', 'Read', 'Update', 'Delete'를 의미한다.
> 그리고 HTTP 메소드에서 GET, POST, PUT, DELETE가 각 CRUD의 역할을 한다.
>
> - Create: POST/PUT
> - Read: GET
> - Update: PUT
> - Delete: DELETE

<br>

#### 1. GET

> GET 메소드는 서버의 데이터를 취득할 때 사용하는 메소드이다. 굉장히 자주 이용되는 메소드이며, Web 페이지, 이미지, 영상 등을 취득할 때 사용한다.
> 아래 예시를 보면 'http://example.com/' 에 요청을 보내게 되고 서버는 지정된 URI에 맞는 데이터를 응답한다.

```xml
// 요청 예시
GET / HTTP / 1.1;
Host: foo.com;
```

> 요청에 본문 존재: 아니오
> 성공 응답에 본문 존재: 예
> 안전함: 예
> 멱등성: 예
> 캐시 가능: 예
> HTML 양식에서 사용 가능: 예
>
> - 멱등성 : 동일한 요청을 한 번 보내는 것과 여러 번 연속으로 보내는 것이 같은 효과를 지니고, 서버의 상태도 동일하게 남을 때, 해당 HTTP 메서드가 멱등성을 가졌다고 말한다.

<br>

#### 2. POST: Create

> POST 메소드는 서버로 데이터를 전송하고, 요청 유형은 Content-Type 헤더로 나타낸다.
>
> 예를 들어, 벨로그에 새로운 게시글을 올릴 때와 같이 새로운 리소스에 데이터를 만들 때 주로 사용한다. 또한 기존의 데이터를 수정할 때도 사용되기도 하며, 다른 메소드로는 할 수 없는 작업일 때 사용되기도 하는데 대표적인 예가 검색결과를 표시하는 URI를 들 수 있다.
>
> 일반적으로는 URI에 검색 키워드를 넣어 GET하는 것이 가능하지만, 키워드가 매우 긴 경우에는 URI를 통해 GET하는 것은 좋지 않다. 이럴 때 POST 메소드를 사용하면 좋다.

```xml
// 요청 예시
POST / HTTP/1.1
Host: foo.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 13

say=Hi&to=Mom
```

> 요청에 본문 존재: 예
> 성공 응답에 본문 존재: 예
> 안전함: 아니오
> 멱등성: 아니오
> 캐시 가능: 신선도 정보 포함 시
> HTML 양식에서 사용 가능: 예

<br>

#### 3. PUT

> PUT 메소드는 요청 페이로드를 사용해 새로운 리소스를 생성하거나, 대상 리소스를 나타내는 데이터를 대체할 때 사용한다.
>
> POST 메소드로 가능한 리소스 생성을 PUT 메소드로도 가능하다. 예를 들어, 존재하지 않는 URI에 PUT 요청을 하면 서버는 새로운 리소스를 생성하게 된다.

```xml
PUT /new.html HTTP/1.1
Host: example.com
Content-type: text/html
Content-length: 16

<p>New File</p>
```

> 요청에 본문 존재: 예
> 성공 응답에 본문 존재: 아니오
> 안전함: 아니오
> 멱등성: 예
> 캐시 가능: 아니오
> HTML 양식에서 사용 가능: 아니오

<br>

#### 4. DELETE

> 메소드 이름 그대로 DELETE 메소드는 특정 리소스를 삭제하는데 사용된다.

```xml
DELETE /file.html HTTP/1.1
```

> 요청에 본문 존재: 아니오
> 성공 응답에 본문 존재: 아니오
> 안전함: 아니오
> 멱등성: 예
> 캐시 가능 아니오
> HTML 양식에서 사용 가능 아니오

<br>
<br>

### 📚 Reference

&nbsp; https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/GET
&nbsp; https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/POST
&nbsp; https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/PUT
&nbsp; https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/DELETE

<br>
<br>
