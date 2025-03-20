---
title: "Web과 WAS, 그리고 Spring 🌱"
categories:
  - NetWork
tags:
  - Web
  - Spring
  - WAS
date: 2025-03-16 00:00:00 +0800
---

<head>
  <link rel="stylesheet" href="{{ '/assets/css/style.css' | relative_url }}">
</head>

<hr class="custom-hr">
<h5 style="text-align: center">웹 서버와 WAS의 차이, 그리고 Spring의 역할 </h5>
<hr class="custom-hr">
<p>
  <img src="/assets/img/network/static.png" alt="Web Server" width="60%" style="display: block; margin: auto;">
</p>

<div>
  <h1>📌 Web Server 란?</h1>
  <p>브라우저로부터 <b>HTTP 요청</b>을 받고 요청에 맞는 <b>정적 콘텐츠</b>를 제공하는 프로그램</p>
  <ul>
    <li>요청값에 상관없이 동일한 콘텐츠 제공 (HTML, CSS, image)</li>
    <li>정적 리소스를 클라이언트에 서빙하는 역할</li>
  </ul>
</div>

<div>
  <h3>✅ Web Server 의 기능</h3>
  <ul>
    <li>클라이언트로부터 <b>HTTP 요청</b>을 받을 수 있음</li>
    <li>정적 콘텐츠 (HTML, CSS, JS, 이미지) 제공</li>
    <li><b>동적 콘텐츠 요청 시 WAS에 전달하여 처리 결과 반환</b></li>
  </ul>
</div>

<div>
<p>
  <img src="/assets/img/network/dynamic.png" alt="Web Server" width="60%" style="display: block; margin: auto;">
</p>
  <h1>📌 WAS 란?</h1>
<ul>
  <li>DB조회나 다양한 비지니스 로직을 처리해 동적인 컨텐츠를 생성하고 제공하기 위해 만들어진 프로그램</li>
  <li>정적 컨텐츠와 다르게 사용자나 인자값이 달라지게 되면 컨텐츠 내용이 바뀔 수 있음</li>
</ul>
</div>

<div>
  <h3>✅ WAS 의 기능</h3>
  <ul>
    <li>클라이언트로부터 <b>HTTP 요청</b>을 받을 수 있음 (대부분의 WAS는 Web Server 내장)</li>
    <li>요청에 맞는 정적 컨텐츠(html, jpeg, css)를 제공할 수 있다.</li>
    <li>DB조회나 다양한 로직 처리를 통해 동적 컨텐츠를 제공할 수 있다.</li>
  </ul>
</div>

<div>
  <h3>✅ Web Server와 WAS를 같이 사용했을 때의 장점</h3>
  <ul>
    <li>책임 분할을 통한 <b>서버 부하</b>를 방지한다. 즉 <b>로드밸런싱(여러대의 WAS)</b>을 사용할 수 있다.</li>
    <li>리버스 프록시(대리자)를 통해 실제 서버를 외부에 노출하지 않을 수 있다.</li>
  </ul>
</div>
<br>

<div>
  <h1>📌 Spring 요청 처리 흐름</h1>
  <img src="/assets/img/network/wasServletContainer.png" alt="Spring Request Flow" width="100%" style="display: block; margin: auto;">
<br>
  <ul>
    <li>
      <b>1️⃣  클라이언트(브라우저) → WAS(Tomcat)</b><br>
      사용자가 웹 브라우저에서 요청을 보내면, 요청이 WAS로 전달된다.  
      WAS는 서블릿을 실행하는 환경을 제공한다.
    </li>
  </ul>
  <ul>
    <li>
      <b>2️⃣  WAS(Tomcat) → Filter → Servlet Container</b>  <br>
      WAS는 요청을 받으면 필터를 거친다.  
      필터는 보안, 인증, 요청/응답 수정 등의 작업을 수행한다.  
      요청이 필터를 통과한 후 서블릿 컨테이너로 전달되며, 서블릿 컨테이너는 서블릿을 실행하고 요청을 처리한다.
    </li>
  </ul>
  <ul>
    <li>
      <b>3️⃣ 서블릿 실행</b>  <br>
      서블릿이 요청을 받아 비즈니스 로직을 수행한다.  
      DB 조회 및 로직 처리를 통해 응답을 생성한다.
    </li>
  </ul>
  <ul>
    <li>
      <b>4️⃣ Servlet Container → 필터 → WAS → 클라이언트</b>  <br>
      응답은 다시 필터를 거쳐 클라이언트(브라우저)로 전달된다.  
      필터는 응답을 수정하거나 로깅할 수도 있다.
    </li>
  </ul>
</div>

<br>

<div>
  <h3>✅ Servlet Container와 Spring🌱 의 관계</h3>
  <ul>
    <li>Servlet Container는 서블릿(Servlet)과 JSP를 실행하는 환경을 제공한다.</li>
    <li>Spring은 서블릿을 기반으로 동작하는 웹 프레임워크이므로, Servlet Container 위에서 실행된다.</li>
    <li>Spring MVC의 핵심인 DispatcherServlet도 결국 서블릿이다.</li>
    <p><b>즉, Spring이 동작하려면 Servlet Container가 필요하며 Spring 자체는 서블릿 컨테이너를 포함하지 않는다.</b></p>
  </ul>

  <h3>✅ Spring Boot의 경우</h3>
  <li>Spring Boot는 Tomcat, Jetty, Undertow 같은 서블릿 컨테이너를 내장하고 있어 별도의 WAS 설치가 필요없다.</li>


<br>
<div>
  <hr>
  <h3>✍️ 마무리 정리</h3>
  <p> <b>Web 서버, WAS, 그리고 Spring의 동작 방식</b>에 대해 공부했다.<br>
  쌤은 Spring의 동작 방식에 대해 좀 더 깊게 알아보라 조언하고 따로 설명해주셨다.<br>
  다음에는 <b>로드 밸런싱과 리버스 프록시</b>에 대해 더 깊이 알아보고 실제 코드로 구현해봐야겠다.</p>
  <hr>
</div>

</div>

