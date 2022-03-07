### 상속 관계에서 @BeforeEach 순서

테스트 코드를 작성하는 도중, 상속 관계에 있을 때 `@BeforeEach`의 순서가 어떻게 동작하는지 궁금해졌다.  
`Documentation extends AcceptanceTest`이며 `@BeforeEach`가 각각의 클래스에 `setUp()`메서드로 존재한다.

![image](https://user-images.githubusercontent.com/54942017/156982943-f04e6660-c1ba-47db-a473-1b33ad345f8c.png)

![image](https://user-images.githubusercontent.com/54942017/156982978-b7a518ad-0aa9-423a-8d32-839606fad5ac.png)

---
### 결과

결과부터 말하자면 제일 상위 클래스의 `@BeforeEach`부터 실행된다.

---
### 과정

디버깅 해본 결과
`ClassBasedTestDescriptor.prepare`메서드에서 답을 찾을 수 있었다.
![image](https://user-images.githubusercontent.com/54942017/156982164-b846bd2c-9ae4-4917-8fad-efff95746fff.png)

`registerBeforeEachMethodAdapters(registry);`라는 메서드가 실행되고 있었고,

![image](https://user-images.githubusercontent.com/54942017/156982267-e18b8a65-f347-40f6-a7ac-07f8451b49ec.png)
`LifecycleMethodUtils.findBeforeEachMethods`에서 실행되어야 하는 @BeforeEach메서드가 TOP_DOWN 방식으로 등록되고 있었다.
![image](https://user-images.githubusercontent.com/54942017/156982356-340f4954-8541-46ba-92cc-e5a972243c70.png)

타고 들어가 보면 내부 로직은 `findAllMethodsInHierarchy()`메서드 재귀호출을 통해서 제일 상위에 있는 `Superclass`의 `@BeforeEach`메서드부터 찾으면서, 하위 `Subclass`까지 찾아서 등록한다.

![image](https://user-images.githubusercontent.com/54942017/156982563-89fa01f8-7aff-4a40-afe7-053fba4f5fef.png)

![image](https://user-images.githubusercontent.com/54942017/156982743-d86ef021-dbfa-404a-ab3c-aaa0dd7933bf.png)




