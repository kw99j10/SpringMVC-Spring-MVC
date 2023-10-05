# SpringMVC

<br>

## 5. Spring MVC 기본 기능 <br>

<h3>●로깅(Logging) </h3>

<h5>SLF4J 인터 페이스를 사용하여 구현체인 로그 라이브러리를 이용 </h5>
<h5>로그 레벨: trace > debug > info > warn > error </h5>
<h5>전체 로그 레벨 설정 기본은 info 수준(개발 서버는 debug 출력)</h5>
<h5>sout처럼 "+" 사용 시 log 실행 전 문자 더하기 연산이 발생하여 자원 낭비가 됨</h5>

<br>
<h4>●로그 사용시 장점</h4>
<h5>로그 레벨에 따라 상황에 맞게 조절 가능</h5>
<h5>콘솔 뿐 아니라 파일, 네트워크 등에 남길 수 있음</h5>
<h5>sout보다 성능이 좋음(내부 버퍼링, 멀티 쓰레드 등)</h5>

<br>
<h4>@RestController</h4>
<h5>반환 값이 String 일 때 @Controller(애노테이션)는 뷰와 뷰 리졸버를 찾음</h5>
<h5>이와 달리 @RestController는 return 타입에 있는 값을 그대로 HTTP 메시지 바디에 입력 </h5>
<h5>@ResponseBody와 관련 있음 </h5>
<br>

<h4>@PathVariable 경로 변수 사용 </h4>
<h5>리소스 경로에 식별자를 넣는 방식 (URL 경로 템플릿화) </h5>
<h5>식별자와 파라미터 이름이 같으면 생략 가능 </h5>
<br>
<h4>●미디어 타입 조건 매핑</h5>
  - consume : content-type 헤더의 타입 기반 매핑 <br>
  - produce : accept 헤더의 타입 기반 매핑
<h5>content-type 헤더는 현재 전송하는 데이터의 타입을 명시 함</h5>
<h5>accept 헤더는 현재 처리할 수 있는 데이터의 타입을 명시 함 </h5>
<br>
<h4>●HTTP 헤더 정보를 조회하는 방법</h4>
<h5>Request 객체, Response 객체, Method, Locale 정보 조회</h5>
<h5>@RequestHeader MultivalueMap: 하나의 key에 여러 value 대응 가능</h5>
<h5>@RequestHeader("host") String host: 특정 HTTP 해더를 조회(ex:host)</h5>
<h5>@CookieValue: 특정 쿠키 조회, 필수 값 여부, 기본 값 설정 가능 </h5>
<br>
<h4>●HTTP 요청 파라미터 </h4>
<h5>요청 파라미터 조회: GET 쿼리 파라미터 전송 방식, POST HTML FORM 전송 방식 </h5>
<h5>1. HTTPServletRequest 객체를 이용하여 전송 </h5>
<h4>2. @RequestParam의 name 속성을 파라미터로 이용하여 전송 </h4>
<h6>@ResponseBody 애노테이션: view 리졸버의 view 조회를 무시 하고, HTTP message body에 직접 해당 내용 입력함</h6>
<h5>2-1. 변수명이 같으면 생략 가능</h5>
<h5>2-2. 파라미터 값이 여러 개 이면 map을 이용하여 여러 개 가능</h5>
<h5>2-3. 애노테이션을 없앨 수도 있음(단순 타입일 경우) </h5>
<h5>2-4. required 값: 기본 값 true, 없으면 에러 cf) 파라미터 이름만 있고 값이 없는 경우: 빈문자로 전송되므로 주의 </h5>
<h5>2-5. default 값 설정 시 required 설정 필요 x, 빈문자여도 default 값 전송 </h5>
<br>
<h4>3.@ModelAttribute를 이용한 객체 전송 </h4>
<h5>파라미터를 바인딩 받을 객체 필요 </h5>
<h5>작동 원리: 객체를 생성 후 해당 객체의 프로퍼티의 setter를 호출하여 파라미터의 값을 입력(바인딩) </h5>
<h5>단순 타입과 argument resolver로 지정한 타입들을 외하고 애노테이션 생략 가능 </h5>
<br>
<h4>●HTTP 요청 메시지 - 단순 텍스트 </h4>
<h5>메시지 바디에 데이터를 직접 꺼냄 - API 통신 시 주로 사용(JSON, XML, TEXT) </h5>
<h5>@RequestParam과 @ModelAttribute 사용할 수 없음  </h5>
<h5>HttpEntoty: 메시지 바디 정보를 직접 조회 & 요청 파라미터 조회 기능과 관계 X </h5>
<h5>응답에도 사용 가능</h5>
<h5>헤더 정보 포함 가능</h5>
<h5> view를 조회하지 않음(뷰 리졸버 실행 X) </h5>
<h5>HttpEntity를 상속받는 객체: RequestEntity, ResponseEntity </h5>
<br>
<h4>@RequestBody</h4>
<h5>HTTP 메시지 바디 정보를 편리하게 조회</h5>
<h5>요청 파라미터 vs HTTP 메시지 바디</h5>
<h6>요청 파라미터를 조회하는 기능: @RequestParam, @ModelAttribute</h6>
<h6>Http 메시지 바디를 직접 조회하는 기능: @RequestBody</h6>
<br>
<h4>@ResponseBody</h4>
<h5>응답 결과를 HTTP 메시지 바디에 직접 담아서 전달/h5>
<h5> view를 조회하지 않음(뷰 리졸버 실행 X) </h5>
<br>
<h4>●HTTP 요청 메시지 - JSON </h4>
<h5>@RequestBody에 직접 만든 객체 지정 가능 </h5>
<h5>@RequestBody는 생략할 수 없음 -> 생략 시 @ModelAttribute가 적용 (위 규칙에 의해) </h5>
<h5>@RequestBody 요청: JSON 요청 -> HTTP 메시지 컨버터 -> 객체</h5>
<h5>@ResponseBody 응답: 객체 -> Http 메시지 컨버터 -> JSON </h5>
<br>

<h4>●HTTP 응답 </h4>
<h5>정적 리소스: 브라우저에 정적인 HTML, css, js를 제공할 때</h5>
<h5>뷰 템플릿 사용: 웹 브라우저에 동적인 HTML을 제공할 때</h5>
<h5>Http 메시지 사용: HTTP API를 제공하는 경우 </h5>
<br>
<h4>정적 리소스</h4>
<h5>스프링 부트가 "src/main/resources/static" 디렉토리에 있는 정적 리소스 제공 </h5>
<h5>해당 파일 변경 없이 그대로 서비스 </h5>
<br>
<h4>뷰 템플릿</h4>
<h5>뷰 템플릿 경로: "src/main/resources/templates" </h5>
<h5>뷰 템플릿을 거쳐서 HTML이 생성되고, 뷰가 응답을 만들어서 전달 </h5>
<h5>String을 반환하는 경우: @ResponseBody 가 없으면 뷰 리졸버가 실행되어서 뷰를 찾고, 렌더링</h5>
<h5>View or Http 메시지: @ResponseBody 가 있으면 뷰 리졸버를 실행하지 않고, HTTP 메시지 바디에 직접 입력.</h5>
<br>
<h4>HTTP API, 메시지 바디 직접 입력</h4>
<h5>정적 리소스나 뷰 템플릿을 거치지 않고, 직접 HTTP 응답 메시지를 전달하는 경우</h5>
<h5>@ResponseStatus 애노테이션을 사용하여 응답 코드 설정 가능 </h5>
<h5>동적으로 변경 시 ResponseEntity를 사용 </h5>
<br>
<h4>@RestController : @ResponseBody + @Controller 로서 Rest API를 만들 때 주로 사용 </h4>
<br>

<h4>●HTTP 메시지 컨버터</h4>
<h5>@ResponseBody 사용 시 HTTP의 BODY에 문자 내용을 직접 반환</h5>
<h5>뷰 리졸버 대신에 HTTP 메시지 컨버터가 동작하여 문자, 객체, byte 등을 처리 </h5>
<br>
<h5>●HTTP 메시지 컨버터를 적용하는 경우 </h5>
<h6>HTTP 요청: @RequestBody, HttpEntity(RequestEntity)</h6>
<h6>HTTP 응답: @ResponseBody, HttpEntity(ResponseEntity)</h6>
<br>
<h5>●스프링 부트 기본 메시지 컨버터 </h5>
<h5>우선순위 </h5>
<h6>0. ByteArrayHttpMessageConverter - 클래스 타입: byte[], 미디어 타입: */* </h6>
<h6>1. StringHttpMessageConverter - 클래스 타입: String, 미디어 타입: */* </h6>
<h6>2. MappingJackson2HttpMessageConverter - 클래스 타입: 객체 or hashMap, 미디어 타입: application/json </h6>
<h5>HTTP 요청 데이터 읽기</h5>
<h6>요청 시 클래스 타입과 미디어 타입(content-type)을 만족하면 read()를 호출하여 객체 생성 & 반환 </h6>
<h5>HTTP 응답 데이터 생성</h5>
<h6>응답 시 클래스 타입과 미디어 타입(accept)을 만족하면 write()를 호출하여 HTTP 응답 메시지 바디에 데이터를 생성</h6>
<br>
<h4>●Argument Resolver</h4>
<h5>컨트롤러의 파라미터, 애노테이션 정보를 기반으로 전달 데이터 생성 </h5>
<h5>supportsParameter()를 호출해서 해당 파라미터를 지원하는지 체크 </h5>
<h5>지원하면 resolveArgument()를 호출해서 실체 객체 생성 -> 컨트롤러 호출</h5>
<br>
<h4>●ReturnValueHandler</h4>
<h5>응답 값을 변환하고 처리 (응답 데이터를 HTTP 메시지에 입력) </h5>
<br>
<h4>●HTTP 메시지 컨버터의 위치 </h4>
<h5>요청의 경우: @RequestBody 와 HttpEntity를 각각 처리하는 ArgumentResolver가 존재</h5>
<h5>응답의 경우: @ResponseBody 와 HttpEntity를 각각 처리하는 ReturnValueHandler가 존재</h5>
<h5>만약 ArgumentResolver와 ReturnValueHandler가 처리할 수 없다면 HTTP 메시지 컨버터를 호출</h5>
<br>
<h5>동작 과정</h5>
<h5>RequestMapping 핸들러 어댑터 -> ArgumentResolver (-->HTTP 메시지 컨버터) </h5>
<h5> -> 핸들러 -> ReturnValueHandler(-->HTTP 메시지 컨버터) -> RequestMapping 핸들러 어댑터 </h5>
<hr>

<br>

## 6. Spring MVC 웹 페이지 만들기 <br>
<h4>●웹 페이지 제작시 병렬적 구조로 작업 진행 </h4>
<br>
<h5>디자이너: 요구사항 디자인 & 결과물 웹 퍼블리셔에게 전달</h5>
<h5>웹 퍼블리셔: 디자인을 기반으로 HTML, CSS를 만들어 백엔드 개발자에게 전달</h5>
<h5>백엔드 개발자: HTML 화면이 나오기 전까지 시스템 설계 및 비지니스 모델 개발, </h5>
<h5>이후 HTML을 뷰 템플릿으로 변환 후 동적 화면 제작 및 웹 화면 흐름 제어 </h5>
<br>

<h4>●데이터 접근 시 중복 보다는 명확성에 초점을 두고 접근할 것</h4>
<br>
<h4>●서비스 운영 시 정적 리소스가 공개될 수 있으므로 static 폴더에 HTML을 넣지 말 것</h4>
<br>
<h4>●타임리프 주요 기능 </h4>
<br>
<h5>타임리프 핵심</h5>
<h6>th:xxx가 붙은 부분은 서버사이드에서 렌더링되어 기존 것을 대체 함</h6>
<h6>th:xxx가 없다면 html의 xxx 속성이 그대로 사용 </h6>
<h6>HTML을 파일 보기를 유지하면서 템플릿 기능을 할 수 있음</h6>
<br>

<h5>속성 변경: th:href="@{......}"</h5>
<h6>타임리프 뷰 템플릿을 거쳐 href을 th:href의 값으로 변경</h6>
<br>

<h5>URL 링크 표현식: "@{...}"</h5>
<h6>쿼리 파라미터도 표현(생성) 가능 </h6>
<br>
<h5>리터럴 대체</h5>
<h6>| ... | 형태로 사용 </h6>
<h6>더하기 없이 편리하게 사용 가능 </h6>
<br>
<h5>변수 표현식</h5>
<h6>"${}": 프로퍼티 접근법 사용</h6>
<br>
<h5>내용 변경: th:text="${}"</h5>
<h6>내용의 값을 th:text 값으로 변경</h6>
<br>
<h5>속성 변경: th:value="${}"</h5>
<h6>프로퍼티 접근 법으로 출력 & value 속성을 th:value 속성으로 변경 </h6>
