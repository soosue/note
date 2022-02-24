# 그냥 노트

---
### enum

![image](https://user-images.githubusercontent.com/54942017/155433514-271a2f76-7ffb-4ea9-b97b-1f6d9672d9bf.png)  
해당 `enum`이 사용될 때, 해당 `enum`의 초기화가 시작됨.  
`enum`상수에 해당하는 객체들을 생성한다. 괄호()안의 속성들은, 해당 객체가 가지고 있을 속성의 값들이다.

이렇게 생각해볼 수도 있다.  
![image](https://user-images.githubusercontent.com/54942017/155434809-e0a2c314-a839-40c3-8800-44368f289066.png)

`FindType`라는 공통성을 가져서, 속성들(`weightFunction`)도 같지만, 속성값(`Section::getDistance`, `Section::getDuration`)들은 다른 싱글톤 객체들(`DISTANCE`, `DURATION`)이 필요할 때 사용할 수 있다.

아래와 같이 상수에 행위(`method`)를 줄 수 있다. 일반 메서드를 `@Override`도 가능.  
![image](https://user-images.githubusercontent.com/54942017/155462155-de66ece3-ecc4-40b2-89c5-27f92036ecb3.png)

`Enum<E>`를 확장중임.  
`Serializable`, `Comparator`를 구현중.

---
