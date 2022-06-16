6-1     
타입  | 변수명 | 설명      
int  | num   |카드 숫자 (1~10 사이 정수)        
boolean | isKwang | 광이면 true, 아니면 false     
위 멤버 변수를 갖는 SutdaCard 클래스 정의        
```java
class sutdaCard{
    int num;
    boolean isKwang;
}
```
6-2     
1번 클래스에 생성자 두개, info() 추가해서 실행결과와 같도록 완성     
실행결과:       
3       
1K
```java
class Exercise6_2{
    public static void main(String args[]){
        SutdaCard card1 = new SutdaCard(3, false);
        sutdaCard card2 = new SutdaCard();

        System.out.println(card1.info());
        System.out.println(card2.info());
    }
}

class SutdaCard{
    int num;
    boolean isKwang;
    
    SutdaCard(){
        this.num = 1;
        this.isKwang = true;
    }
    
    SutdaCard(int num, boolean isKwang){
        this.num = num;
        this.isKwang = isKwang;
    }
    
    String info() {
        return num + (isKwang? "K": ""); 
        // int num은 문자열과 연산되면서 최종적으로 문자열 반환
    }
}
```
6-3     
다음 멤버변수를 갖는 Student 클래스 정의      
타입, 변수명, 설명     
String name 학생이름        
int ban 반       
int no 번호       
int kor 국어점수        
int eng 영어점수        
int math 수학점수       
```java
class Student{
    String name;
    int ban;
    int no;
    int kor;
    int eng;
    int math;
}
```
6-4     
3문에서 정의한 Student 클래스에 다음 두 매소드 getTotal(),getAverage()추가
```java
class Exercise6_4 {
    public static void main(String args[]) {
        Student s = new Student(); s.name = "홍길동";
        s.ban = 1;
        s.no = 1;
        s.kor = 100; s.eng = 60; s.math = 76;
        System.out.println("이름:"+s.name); 
        System.out.println("총점:"+s.getTotal()); 
        System.out.println("평균:"+s.getAverage());
    }
}
class Student{
    String name;
    int ban;
    int no;
    int kor;
    int eng;
    int math;
    
    int getTotal(){
        return kor + eng + math;
    }
    float getAverage(){
        return (int)(getTotal() / 3f * 10 * 10f) /10f;
    }
}
```

```java
```

```java
```

```java
```

```java
```

```java
```

```java
```

```java
```

```java
```

```java
```

```java
```