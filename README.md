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
