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
