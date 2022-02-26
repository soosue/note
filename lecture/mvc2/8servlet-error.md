# 서블릿 예외 처리

## Servlet이 예외를 처리하는 경우는 아래 2가지 경우이다.
1. `Exception`이 발생할 때
2. `response.sendError()`를 호출할 때  

`1`의 경우가 발생하면 WAS까지 예외가 전파되고, `ErrorPage`에 등록되어 있는 주소를 다시 호출한다.  
`2`의 경우 정상적으로 처리되어 WAS까지 오고, `sendError()`호출 기록에 따라 `ErrorPage`에 등록되어 있는 주소를 다시 호출한다.  

결과적으로 서블릿 내부에서 요청이 2번 일어나는 것과 같게 되며, 문제는 없지만 경우에 따라 `Servlet Filter`와 `Spring Interceptor`가 2번 호출될 수 있다.

### Servlet Filter 호출 제외하기
`Filter`는 `DispatcherType`을 지정할 수 있으며, 기본적으로는 `Request`만 받게 되어있고, 위와 같은 예외상황의 경우 `Error`로 넘어가게 된다.

### Spring Interceptor 호출 제외하기
`Interceptor`는 `DispatcherType`을 지정할 순 없지만, `excludePathPatterns()`를 이용하여 호출 안하게 할 수 있다.

### 에러페이지 처리하기
`Spring`에서는 간단하게 처리할 수 있도록 이미 구현이 되어있으며, `BasicErrorController`를 사용할 수 있다.  

뷰 템플릿 `resources/templates/error/xxx.html`  
정적 리소스 `resources/static/error/xxx.html`  
적용 대상이 없을 때 `resources/templates/error.html`

순서대로 우선 순위가 적용된다.
