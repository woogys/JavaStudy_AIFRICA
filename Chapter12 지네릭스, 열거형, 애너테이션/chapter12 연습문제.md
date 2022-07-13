12-1

```
클래스 Box가 다음과 같이 정의되어 있을 때, 
다음 중 오류가 발생하는 문장은? 
경고가 발생하는 문장은?
```

```java
class Box<T> { // 제네릭 타입 T를 선언
    T item;
    
    void setItem(T item) {
        this.item = item;
    }
    T getItem() {
        return item;
    }
}
```

```
a,b,c

a. Box<Object> b = new Box<String>();
Object, Stiring 대입된 타입이 다르므로 오류 발생

b. Box<Object> b = (Object)new Box<String>(); 
(object) 타입을 Box<Object> 타입 참조변수에 대입 불가
Box<String>이 Box<Object>로 형변환 될 수 없음을 의미.

c. new Box<String>().setItem(new Object()); 
대입된 타입은 String, setItem 타입은 Object 이므로 허용 불가

d. new Box<String>().setItem("ABC");
String 타입에 해당하는 문자열 "ABC"가 매개변수이므로 굿굿
```


12-2

```
제네릭 메서드 makeJuice()가 아래와 같이 정의되어 있을 때, 
이 메서드를 올바르게 호출한 문장을 모두 고르시오. 
(Apple과 Grape는 Fruit의 자손이라고 가정하자.)
```

```java
class Juicer {
    static <T extends Fruit> String makeJuice(FruitBox<T> box) {
        String tmp = "";
        for (Fruit f : box.getList()) tmp += f + " ";
        return tmp;
    }
}
```

```
타입 T를 요소로 하는 FruiteBox를 매개변수로 허용한다.
이때 T는 Fruit와 그 자손들만 가능하도록 제한.
p.685

c,d

a. Juicer.<Apple>makeJuice(new FruitBox<Fruit>());
제네릭 메소드에 대입된 타입은 Apple. 따라서 매개변수는 FruitBox<Apple>
타입이 된다. 문제는 FruitBox<Fruit>이라고 했으므로 에러.

b. Juicer.<Fruit>makeJuice(new FruitBox<Grape>()); 
타입이 다르면 Fruit와 Grape가 부모-자식 관계에 있어도 에러 발생

c. Juicer.<Fruit>makeJuice(new FruitBox<Fruit>()); 
타입 일치된 상태.

d. Juicer.makeJuice(new FruitBox<Apple>());
제네릭 메소드 타입 호출이 생략된 형태. 타입 일치 상태 

e. Juicer.makeJuice(new FruitBox<Object>());
<T extends Fruit>로 제한이 걸려 있으므로, Fruit과 그 자손만 
해당한다. Object는 해당 없음.

```

12-3

```
올바르지 않은 문장 모두 고르기
```

```java
class Box<T extends Fruit> { // 제네릭 타입 T를 선언
    T item;

    void setItem(T item) {
        this.item = item;
    }

    T getItem() {
        return item;
    }
}
```

```
c, d, g

a. Box<?> b = new Box();
Ok. Box<?> = Box<? extends Object> 같은 형태.
new Box<>();이 더 올바른 형태긴 하지만 a처럼 써도 무방

b. Box<?> b = new Box<>();
Ok. 타입이 생략된 형태. 생략 시 참조변수 타입과 같은 것으로 간주
문제에서 <T extends Fruit>으로 제한이 걸려 있으므로 
Fruit이 생략된 걸로 봐야 함

c. Box<?> b = new Box<Object>();
Object는 Fruit 자식 클래스가 아니므로 대입 불가.

d. Box<Object> b = new Box<Fruit>();
타입이 다르므로 대입 불가

e. Box b = new Box<Fruit>();
가능은 하나, 바람직하지 않음

f. Box<? extends Fruit> b = new Box<Apple>();
일반적인 형태

g. Box<? extends Object> b = new Box<? extends Fruit>();
new 연산자에는 와일드카드 사용 불가
```

12-4

```
아래 메소드는 두 개의 ArrayList를 매개변수로 받아서, 하나의 새로운 
ArrayList로 병합하는 메소드다. 제네릭 메소드로 변경할 것 p.686
```
변경 전
```java
 public static ArrayList <? extends Product> merge (
        ArrayList<? extends Product> list, ArrayList<?extends Product> list2) {
              ArrayList<? extends Product> newList = new ArrayList<>(list);
        
              newList.addAll(list2);
              return newList;
}
```
변경 후
```java
public static <T extends Product> ArrayList<T> merge (
        ArrayList<T> list, ArrayList<T> list2) {
            ArrayList<T> newList = new ArrayList<>(list);
            
            newList.addAll(list2);
            return newList;
        }
        
```

12-5

```
예제7-3에 열거형 Kind와 Number를 새로 정의하여 적용한 것.
(1)에 알맞은 코드를 넣어 완성
```

```java
class Exercise12_5 {
    public static void main(String args[]) {
        Deck d = new Deck(); // 카드 한 벌(Deck)을 만든다.
        Card c = d.pick(0); // 섞기 전에 제일 위의 카드를 뽑는다.
        System.out.println(c); // System.out.println(c.toString());과 같다.

        d.shuffle(); // 카드를 섞는다.
        c = d.pick(0); // 섞은 후에 제일 위의 카드를 뽑는다.
        System.out.println(c);
    }
}

class Deck {
    final int CARD_NUM = Card.Kind.values().length * Card.Number.values().length; // 카드의 개수
    Card cardArr[] = new Card[CARD_NUM]; // Card 객체 배열을 포함

    Deck() {
        
        /* (1) 알맞은 코드를 넣어서 완성하시오 .
                Deck의 카드를 초기화한다.
         */
        
        int i = 0; // i 초기화

        for(Card.Kind kind : Card.Kind.values()) {
            for(Card.Number num : Card.Number.values()) {
                cardArr[i++] = new Card(kind, num);
            }
        }
    }

    Card pick(int index) { // 지정된 위치(index)에 있는 카드 하나를 꺼내서 반환
        return cardArr[index];
    }

    void shuffile() { //카드 순서를 섞는다. 
        int i = 0; //여기서도 초기화 안해주면 에러 발생함
        
        for (i = 0; i < cardArr.length; i++) {
            int r = (int) (Math.random() * CARD_NUM);

            Card temp = cardArr[i];
            cardArr[i] = cardArr[r];
            cardArr[r] = temp;
        }
    }
} // Deck 클래스의 끝

//Card 클래스
class Card {
    enum Kind {CLOVER, HEART, DIAMOND, SPADE}

    enum Number {
        ACE, TWO, THREE, FOUR, FIVE,
        SIX, SEVEN, EIGHT, NINE, TEN,
        JACK, QUEEN, KING
    }

    Kind kind;
    Number num;

    Card() {
        this(Kind.SPADE, Number.ACE);
    }

    Card(Kind kind, Number num) {
        this.kind = kind;
        this.num = num;
    }

    public String toString() {
        return "[" + kind.name() + "," + num.name() + "]";
    } //toString()의 끝
} // Card 클래스의 끝
```

```
실행 결과
[CLOVER,ACE]
[SPADE,FOUR] // 실행 시 마다 랜덤
```

12-6

```
다음 중 메타 애너테이션이 아닌 것 모두 고르기
```

```
c.

a. Documented
b. Target
c. Native
d. Inherited

메타 어노테이션은 어노테이션을 위한 어노테이션으로, 
어노테이션을 정의할 때 적용 대상이나 유지 기간 등을 
지정하는 데 사용된다. 
java.lang.annotation 패키지에 포함되어 있다. 

@Target, @Documented, @Inherited,
@Retention, @Repeatable 
```

12-7

```
TestInfo가 다음과 같이 정의되어 있을 때, 
이 어노테이션이 올바르게 적용되지 않은 것은?
```

```java
@interface TestInfo {
    int count() 
            default 1;
    
    String[] value() 
            default "aaa";
}
```

```
b,d

a. @TestInfo              class Exercise12_7{}
디폴트 값이 지정된 요소는 어노테이션 적용시 값 생략 가능

b. @TestInfo(1)           class Exercise12_7{}
@TestInfo(count = 1)로 써야 한다. 요소 이름이 value인 
경우에만 선지와 같이 생략 가능

c. @TestInfo("bbb")       class Exercise12_7{}
@TestInfo(count=1, value={"bbb"})가 생략된 형태
요소 이름이 value인 bbb는 생략 가능하다.

d. @TestInfo("bbb","ccc") class Exercise12_7{}
요소 타입이 배열이고, 지정 값이 여러개이면 {}가 필요하다.
@TestInfo({"bbb", "ccc"}) 처럼 쓰거나,
@TestInfo(value={"bbb","ccc"})가 올바르다.

```
