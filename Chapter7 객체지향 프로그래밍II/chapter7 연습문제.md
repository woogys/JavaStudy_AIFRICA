7-1		
섯다 카드 20장을 담는 SutdaCard 배열 초기화. 1~10까지 숫자가 한 쌍씩 있고,     
1,3,8은 둘중 하나가 광(kwang)이어서, SutdaCard의 인스턴스 변수 isKwang 값이 true여야 함.
```java
class SutdaDeck {
    final int CARD_NUM = 20;
    SutdaCard[] cards = new SutdaCard[CARD_NUM];
    
    SutdaDeck() {
        //(1) 배열 SutdaCard를 적절히 초기화 하시오. 
        
        for(i=0; i<cards.length; i++){
            int num = i%10+1; // 1부터 10까지 숫자가 한쌍씩 있다고 했으므로, 
            // 1부터 19까지 10으로 나눈 나머지만 취해서 +1을 해주면 카드가 마련된다. 
            boolean isKwang = (i<10)&&(num==1||num==3||num==8); 
            // 광은 1,3,8 쌍 중 하나씩 있으므로 범위를 1<10으로 지정하고 1||3||8 중 하나로 지정. 
            cards[i] = new SutdaCard(num, isKwang);
        }
    }
}
class SutdaCard {
    int num;
    boolean isKwang;

    SutdaCard() {
        this(1, true);
    }

    SutdaCard(int num, boolean isKwang) {
        this.num = num;
        this.isKwang = isKwang;
    }

    // info()대신 Object클래스의 toString()을 오버라이딩했다. 
    public String toString() {
        return num + (isKwang ? "K" : "");
    }
}
class Exercise7_1 {
    public static void main(String args[]) {
        SutdaDeck deck = new SutdaDeck();
        
        for(int i=0; i < deck.cards.length;i++) 
            System.out.print(deck.cards[i]+",");
    }
}
```


7-2     
sutdaDeck 클래스에 정의대로 새 메소드 추가 및 테스트      

1.메서드명 : shuffle      
기 능 : 배열 cards에 담긴 카드의 위치를 뒤섞는다.(Math.random()사용)        
반환타입 : 없음       
매개변수 : 없음       

2.메서드명 : pick       
기 능 : 배열 cards에서 지정된 위치의 SutdaCard를 반환한다.       
반환타입 : SutdaCard        
매개변수 : int index - 위치       

3.메서드명 : pick       
기 능 : 배열 cards에서 임의의 위치의 SutdaCard를 반환한다.(Math.random()사용)      
반환타입 : SutdaCard        
매개변수 : 없음       


```java
class SutdaDeck {
final int CARD_NUM = 20;
SutdaCard[] cards = new SutdaCard[CARD_NUM];

    SutdaDeck() {
        for (int i = 0; i < cards.length; i++) {

            int num = i % 10 + 1;
            boolean isKwang = (i < 10) && (num == 1 || num == 3 || num == 8);

            cards[i] = new SutdaCard(num, isKwang);
        }
    }

/* (1) 위에 정의된 세 개의 메서드를 작성하시오.*/
    void shuffle(){
        for(int i=0; i<cards.length; i++){
            int j = (int)(Math.random()*cards.length);
            
            SutdaCard tmp = cards[i];
            cards[i] = cards[j];
            cards[j] = tmp;
        }
    }
    
    SutdaCard pick(int index) { // 배열에서 지정된 위치의 카드를 반환
        if(index <0 || index >=CARD_NUM) // 유효성 검사
            return null;
        return cards[index];
    }
    
    SutdaCard pick(){ // math.random 메소드를 사용해 임의의 카드를 선택후 반환
        int index = (int)(Math.random()*cards.length);
        return pick(index);
    }
    

} // SutdaDeck

class SutdaCard { 
    int num;
    boolean isKwang;
    
    SutdaCard(){
        this(1, true);
    }
    
    SutdaCard(int num, boolean isKwang){
        this.num = num;
        this.isKwang = isKwang;
    }
    
    public String toString() {
        return num + (isKwang ? "K": "");
    }
}
class Exercise7_2 {
    public static void main(String args[]) {
        SutdaDeck deck = new SutdaDeck();

        System.out.println(deck.pick(0)); 
        System.out.println(deck.pick()); 
        deck.shuffle();

        for(int i=0; i < deck.cards.length;i++) 
            System.out.print(deck.cards[i]+",");

        System.out.println(); 
        System.out.println(deck.pick(0));
    }
}

```

7-3     
```
오버라이딩은 수퍼 클래스에 정의된 메소드와 같은 메소드를 서브 클래스에 맞게 재정의하는 것이다. 
상속받은 메소드를 그대로 사용하기도 하지만, 서브 클래스 자신에게 맞게 변경해야 하는 경우가 많고,
이때 오버라이딩이 필요하다.
```

7-4     
```
다음 중 오버라이딩의 조건으로 옳지 않은 것은? (모두 고르시오) 
a. 조상의 메서드와 이름이 같아야 한다.
b. 매개변수의 수와 타입이 모두 같아야 한다.
c. 접근 제어자는 조상의 메서드보다 좁은 범위로만 변경할 수 있다.
d. 조상의 메서드보다 더 많은 수의 예외를 선언할 수 있다.

c: public>protected>default>private 일때, 
조상이 protected라면 자손은 조상과 같거나 넓은 범위인 public, protected만 선택 가능하다.
d: 예외 역시 접근제어자와 마찬가지로 더 적은 수의 예외만 선언할 수 있다.  
```

7-5     
컴파일시 에러가 발생하는 이유를 설명하고, 에러가 발생하지 않도록 수정.
```java
class Product { 
    int price; // 제품의 가격
    int bonusPoint; // 제품구매 시 제공하는 보너스점수
    
    product(){  // product 클래스에 기본 생성자 추가
    }
    
    Product(int price) { 
        this.price = price;
        bonusPoint =(int)(price/10.0);
    }
}

class Tv extends Product { 
    Tv() {}
    public String toString() {
        return "Tv";
    }
}

class Exercise7_5 {
    public static void main(String[] args) {
        Tv t = new Tv();
    }
}
```

7-6     

```
Q.자손 클래스의 생성자에서 조상 클래스의 생성자를 호출해야하는 이유는 무엇인가?
A.자손 클래스 인스턴스 생성 시 조상,자손 멤버가 합쳐진 하나의 인스턴스 생성
이때, 자손 클래스 인스턴스는 조상 클래스 멤버를 전부 사용할 수 있는데,
조상 클래스 초기화를 위해 기본 생성자를 추가해준다.
이렇게 초기화된 조상 클래스의 생성자를 통해 자손이 상속받은 인스턴스 변수의 초기화는
조상 클래스의 생성자가 바로 처리하게 되었다.   
```

7-7     
다음 코드를 실행했을 때 호출되는 생성자 순서와 실행 결과?

```java
class Parent {
    int x = 100;

    Parent() {
        this(200);
    }

    Parent(int x) {
        // super(); 컴파일러가 Object() 자동 호출 
        this.x = x;
    }

    int getX() {
        return x;
    }
}

class Child extends Parent {
    int x = 3000;
    
    Child() {
        this(1000);
    }

     Child(int x) {
        // super(); 컴파일러가 Parent()자동 호출
         this.x = x;
 }
}

class Exercise7_7 {
    public static void main (String[] args) {
        Child c = new Child();

        System.out.println("x="+c.getX());
    }
}
```
```
- 호출되는 생성자 순서 : Child() -> Child(int x) -> Parent() -> Parent(int x) -> Object()
- 실행 결과 : x = 200 
getX 는 Parent 클래스에 정의된 것이므로 Parent 클래스에 있는 인스턴스 변수 x인 200을 리턴한다.
```

7-8

```
다음 중 접근제어자를 접근범위가 넓은 것에서 좁은 것의 순으로 바르게 나열한 것은?
a. public-protected-(default)-private 
b. public-(default)-protected-private 
c. (default)-public-protected-private 
d. private-protected-(default)-public

a. public: 전체 / protected: 같은 클래스 내, 같은 패키지 내, 자식 클래스 / 
default: 같은 클래스 내, 같은 패키지 내 / private: 같은 클래스 내 
```

7-9

```
다음 중 제어자 final을 붙일 수 있는 대상과 붙였을 때 그 의미를 적은 것이다. 옳지 않은 것은? (모두 고르시오)
a. 지역변수 - 값을 변경할 수 없다.
b. 클래스 - 상속을 통해 클래스에 새로운 멤버를 추가할 수 없다. 
c. 메서드 - 오버로딩을 할 수 없다.
d. 멤버변수 - 값을 변경할 수 없다.

c.
오버로딩 X, 상속이 불가능해 메소드를 재정의하는 오버라이딩을 할 수 없다. 
```

7-10        
MyTv2 클래스 멤버변수 isPowerOn, channel, volume를 외부 접근 불가능하게 접근제어자를 붙이고,      
이 멤버변수들의 값을 어디서나 읽고 변경할 수 있도록 getter, setter 추가

```java
class MyTv2 {
    private boolean isPowerOn; // 외부 접근 불가하도록 접근 제어자 private 설정
    private int channel;
    private int volume;

    final int MAX_VOLUME = 100;
    final int MIN_VOLUME = 0;
    final int MAX_CHANNEL = 100;
    final int MIN_CHANNEL = 1;

    //(1) 알맞은 코드를 넣어 완성하시오.
    public void setVolume(int volume){  // volume setter
        if(volume > MAX_VOLUME || volume < MIN_VOLUME)
            return; // 파라미터가 있는 경우에는 값의 유효성 검사 필수
        
        this.volume = volume;
    }
    
    public int getVolume(){ // volume getter
        return volume;
    }
    
    public void setChannel(int channel){ // channel setter
        if(channel > MAX_CHANNEL || channel < MIN_CHANNEL) 
            return; // 파라미터가 있는 경우에는 값의 유효성 검사 필수
        
        this.channel = channel;
    }
    
    public int getChannel(){ // channel getter
        return channel;
    }
    
}

class Exercise7_10 {
    public static void main(String args[]) {
        MyTv2 t = new MyTv2();

        t.setChannel(10);
        System.out.println("CH:" + t.getChannel());
        t.setVolume(20);
        System.out.println("VOL:" + t.getVolume());
    }
}
```

7-11        
문제 10 코드에 아래 조건과 같이 메소드 추가로 실행 결과와 같은 리턴값 만들기
```
메서드명 : gotoPrevChannel
기 능 : 현재 채널을 이전 채널로 변경한다. 
반환타입 : 없음
매개 변수 : 없음
```

```java
class MyTv2 {
    private boolean isPowerOn; 
    private int channel;
    private int volume;
    private int previousChannel; // 이전 채널 저장할 멤버변수

    final int MAX_VOLUME = 100;
    final int MIN_VOLUME = 0;
    final int MAX_CHANNEL = 100;
    final int MIN_CHANNEL = 1;

    public void setVolume(int volume){ 
        if(volume > MAX_VOLUME || volume < MIN_VOLUME)
            return;
        
        this.volume = volume;
    }
    
    public int getVolume(){ 
        return volume;
    }
    
    public void setChannel(int channel){ 
        if(channel > MAX_CHANNEL || channel < MIN_CHANNEL) 
            return; 
        
        previousChannel = this.channel; //  현재 채널을 이전 채널에 저장
        this.channel = channel;
    }
    
    public int getChannel(){ 
        return channel;
    }
    
    public void  gotoPrevChannel() {
        setChannel(previousChannel); // 현재 채널을 이전 채널로 변경하는 매소드
    }
}

class Exercise7_10 {
    public static void main(String args[]) {
        MyTv2 t = new MyTv2();

        t.setChannel(10);
        System.out.println("CH:" + t.getChannel());
        t.setVolume(20);
        System.out.println("VOL:" + t.getVolume());
        t.gotoPrevChannel(); 
        System.out.println("CH:"+t.getChannel()); 
        t.gotoPrevChannel();
        System.out.println("CH:"+t.getChannel());
    }
}
```

```
실행 결과
CH:10
CH:20
CH:10
CH:20
```

7-12

```
다음 중 접근 제어자에 대한 설명으로 옳지 않은 것은? (모두 고르시오) 
a. public은 접근제한이 전혀 없는 접근 제어자이다.
b. (default)가 붙으면, 같은 패키지 내에서만 접근이 가능하다.
c. 지역변수에도 접근 제어자를 사용할 수 있다.
d. protected가 붙으면, 같은 패키지 내에서도 접근이 가능하다.
e. protected가 붙으면, 다른 패키지의 자손 클래스에서 접근이 가능하다.

c.
접근 제어자는 클래스, 멤버변수, 메소드, 생성자에 붙일 수 있으므로 지역변수에 사용할 수 있다는 c의 설명은 틀렸다. 
```

7-13        
Math클래스의 생성자는 접근 제어자가 private인 이유?
```
Math 클래스는 몇 개의 상수와 Static 메소드만으로 구성되어 있어 인스턴스를 생성할 필요가 없다.
따라서 외부에서 불필요하게 접근하는 것을 막기 위해 생성자의 접근 제어자가 private이다.
public final class Math {
    private Math() {}
}
```

7-14        
1번 문제 코드에서 섯다카드 숫자와 종류가 한전 지정되면 변경되지 않도록 수정

```java
class SutdaCard {
    private int num; // 접근제어자를 private으로 변경!
    private boolean isKwang;

    SutdaCard() {
        this(1, true);
    }

    SutdaCard(int num, boolean isKwang) {
        this.num = num; // 인스턴스 변수의 초기화는 선언시가 아니라 여기처럼 생성자에서 가능.
        this.isKwang = isKwang; // 생성자에서 초기화는 단 한번만 이뤄진다.
    }

    public String toString() {
        return num + (isKwang ? "K" : "");
    }
}
class Exercise7_1 {
    public static void main(String args[]) {
        SutdaDeck deck = new SutdaDeck();
        
        for(int i=0; i < deck.cards.length;i++) 
            System.out.print(deck.cards[i]+",");
    }
}
```

7-15        
다음 정의된 클래스 중 형변환을 올바르게 하지 않은 것? (모두 고르시오)
```java
class Unit {}
class AirUnit extends Unit {} 
class GroundUnit extends Unit {} 
class Tank extends GroundUnit {} 
class AirCraft extends AirUnit {}

Unit u = new GroundUnit(); 
Tank t = new Tank();
AirCraft ac = new AirCraft();
```
```
a. u = (Unit)ac;
b. u = ac; //형변환 생략 가능, 업캐스팅
c. GroundUnit gu = (GroundUnit)u;
d. AirUnit au = ac;
e. t = (Tank)u;
f. GroundUnit gu = t;

        Unit
    ↑           ↑
 AirUnit    GroundUnit
    ↑           ↑
 AirCraft      Tank 
 
 e.
 상속도를 보면 파악할 수 있듯이, 유닛은 최상위 클래스이므로, 조상 클래스를 자식 타입으로 형변환 하는 것은 불가능하다.
 
```
7-16        
연산 결과가 true가 아닌 것? (모두 고르시오)
```java
class Car {}
class FireEngine extends Car implements Movable {} 
class Ambulance extends Car {}

FireEngine fe = new FireEngine();
```
```
 a. fe instanceof FireEngine
 b. fe instanceof Movable
 c. fe instanceof Object
 d. fe instanceof Car
 e. fe instanceof Ambulance
 
e.
instanceOf는 어떤 클래스를 상속받았는지 확인하는 연산자로, 상속 관계에 있으면 true를 반환한다.

        Object
          ↑ 
         Car
     ↑           ↑      
Ambulance     FireEngine

상속 관계가 위와 같으므로 fe는 Ambulance와 상속관계에 있지 않아 false가 리턴될 것이다. 
```

7-17        
아래 세개 클래스에서 공통부분을 뽑아 Unit 클래스를 만들고, 이를 상속 받도록 코드 변경
```java
 class Marine { // 보병
    int x, y; // 현재 위치 
    void move(int x, int y) // 지정된 위치로 이동 
    void stop() // 현재 위치에 정지
    void stimPack() //스팀팩을 사용한다.
}
class Tank { // 탱크
    int x, y; // 현재 위치 
    void move(int x, int y) // 지정된 위치로 이동 
    void stop() // 현재 위치에 정지
    void changeMode() // 공격 모드를 변환한다.
}

class Dropship { // 수송선 
    int x, y; // 현재 위치
    void move(int x, int y) // 지정된 위치로 이동 
    void stop() // 현재 위치에 정지
    void load() //선택된 대상을 태운다.
    void unload() // 선택된 대상을 내린다.
}
```

```java
abstract class Unit {
    int x, y;
    abstract void move(int x, int y);
    void stop();
}

class Marine extends Unit {
    void move(int x, int y);
    void stimPack();
}

class Tank extends Unit{
    void move(int x, int y);
    void changeMode();
}

class Dropship extends Unit{
    void move(int x, int y);
    void load();
    void unload();
}
```

7-18        
주어진 실행 결과를 얻도록 코드 완성        
(instanceOf 연산자를 사용해 형변환!)
```
메서드명 : action 
기 능 : 주어진 객체의 메서드를 호출한다.
       DanceRobot인 경우, dance()를 호출하고,
       SingRobot인 경우, sing()을 호출하고,
       DrawRobot인 경우, draw()를 호출한다.
반환타입 : 없음
매개변수 : Robot r - Robot인스턴스 또는 Robot의 자손 인스턴스
```

```java
class Exercise7_18 {
   // (1) action메서드를 작성하시오. 
    public static void action(Robot r) {
        if (r instanceof DanceRobot) {
            DanceRobot dr = (DanceRobot) r;
            dr.dance();
        } else if (r instanceof SingRobot){
            SingRobot sr = (SingRobot) r;
            sr.sing();
        } else if (r instanceof DrawRobot){
            DrawRobot dr = (DrawRobot) r;
            dr.draw();
        }
    }

    public static void main(String[] args) {
        Robot[] arr = { new DanceRobot(), new SingRobot(), new DrawRobot()};

        for(int i=0; i< arr.length;i++) 
            action(arr[i]);
    } // main
}

class Robot {}

class DanceRobot extends Robot {
    void dance() {
        System.out.println("춤을 춥니다.");
    }
}

class SingRobot extends Robot {
    void sing() {
        System.out.println("노래를 합니다.");
    }
}

class SingRobot extends Robot {
    void sing() {
        System.out.println("노래를 합니다.");
    }
}
```

```
실행결과
춤을 춥니다. 
노래를 합니다. 
그림을 그립니다.
```

7-19        
멤버변수로 money, cart를 가진 Buyer 클래스가 있음.                
제품 구입 기능의 buy 메소드, 카트에 구입한 물건을 추가하는 add 메소드,        
구입 목록, 사용금액, 남은 금액을 출력하는 summary 메소드 작성
```
1. 메서드명 : buy 
기 능 : 지정된 물건을 구입한다. 
가진 돈(money)에서 물건의 가격을 빼고, 장바구니(cart)에 담는다.
만일 가진 돈이 물건의 가격보다 적다면 바로 종료한다.
반환타입 :  없음
매개변수 : Product p - 구입할 물건

2. 메서드명 : add
기 능 : 지정된 물건을 장바구니에 담는다.
만일 장바구니에 담을 공간이 없으면, 장바구니의 크기를 2배로 늘린 다음에 담는다.
반환타입 :  없음
매개변수 : Product p - 구입할 물건

3. 메서드명 : summary
기 능 : 구입한 물건의 목록과 사용금액, 남은 금액을 출력한다.
반환타입 :  없음
매개변수 : 없음
```

```java
class Exercise7_19 {
public static void main(String args[]) {
    Buyer b = new Buyer(); 
    b.buy(new Tv()); 
    b.buy(new Computer()); 
    b.buy(new Tv()); 
    b.buy(new Audio()); 
    b.buy(new Computer()); 
    b.buy(new Computer()); 
    b.buy(new Computer());
    b.summary();
    }
}

class Buyer {
    int money = 1000;
    Product[] cart = new Product[3]; // 구입한 제품을 저장하기 위한 배열
    int i = 0; // Product배열 cart에 사용될 index

    void buy(Product p) {
        /* 
        (1) 아래의 로직에 맞게 코드를 작성하시오.
        1.1 가진 돈과 물건의 가격을 비교해서 가진 돈이 적으면 메서드를 종료한다. 
        1.2 가진 돈이 충분하면, 제품의 가격을 가진 돈에서 빼고
        1.3 장바구니에 구입한 물건을 담는다.(add메서드 호출)
         */
        if(money < p.price){
            System.out.println("잔액이 부족합니다."+p+"를 구매할 수 없습니다.");
            return;
        }
        money -= p.price;
        add(p);
    }
    
    void add(Product p) {
         /* 
      (2) 아래의 로직에 맞게 코드를 작성하시오.
        1.1 i의 값이 장바구니의 크기보다 같거나 크면
            1.1.1 기존의 장바구니보다 2배 큰 새로운 배열을 생성한다. 
             1.1.2 기존의 장바구니의 내용을 새로운 배열에 복사한다. 
             1.1.3 새로운 장바구니와 기존의 장바구니를 바꾼다.
        
        1.2 물건을 장바구니(cart)에 저장한다. 그리고 i의 값을 1 증가시킨다.
        */ 
        if(i>= cart.length){
            Product[] twice = new Product[cart.length*2];
            System.arraycopy(cart, 0, twice, 0, cart.length);
            // 괄호 안은 차례대로 복사하고자 하는 원본소스, 원본 소스에서 어느부분부터 읽어 올 것인지, 
            // 복사하려는 대상 소스, 복사를 어느 부분부터 쓸 것인지, 원본에서 복사본까지 데이터를 얼마만큼 읽어올 것인지를 의미. 
            cart = twice;
        }
        cart[i++] = p;
    } // add(Product p)

    void summary() {
        /* 
        (3) 아래의 로직에 맞게 코드를 작성하시오.
        1.1 장바구니에 담긴 물건들의 목록을 만들어 출력한다. 
        1.2 장바구니에 담긴 물건들의 가격을 모두 더해서 출력한다.
        1.3 물건을 사고 남은 금액(money)를 출력한다.
         */
        String itemList = ""; // 물건 목록 초기화
        int sum = 0; //사용 금액 초기화
        
        for (i=0; i< cart.length; i++) {
            if (cart[i]==null) // 
                breat;
            itemList =+ cart[i] = ",";
            sum += cart[i].price;
        }

        System.out.println("구입한 물건:"+itemList);
        System.out.println("사용 금액:"+sum);
        System.out.println("남은 금액:"+money);
    } //summary()
}

class Product {
    int price; // 제품의 가격
    
    Product(int price) {
        this.price = price;

    }
}
class Tv extends Product { 
    Tv() { super(100); }
    
    public String toString() { return "Tv"; }
}

class Computer extends Product { 
    Computer() { super(200); }
    
    public String toString() { return "Computer";}
}

class Audio extends Product { 
    Audio() { super(50); }
    
    public String toString() { return "Audio"; }
}
```

```
실행결과
잔액이 부족하여 Computer을/를 살수 없습니다.
구입한 물건:Tv,Computer,Tv,Audio,Computer,Computer, 
사용한 금액:850
남은 금액:150
```


7-20 ★        
코드 실행 결과?
```java
class Exercise7_20 {
    public static void main(String[] args) {
        Parent p = new Child(); // 참조변수 p,c 모두 Child 인스턴스를 참조한다. 
        Child c = new Child(); 
        
        System.out.println("p.x = " + p.x); // 인스턴스 변수인 x는 참조변수 타입에 따라 달라진다.
        p.method(); // 메소드는 참조변수 타입과 관계 없이 실제 인스턴스 타입인 Child 클래스에 정의된 메소드 호출
        
        System.out.println("c.x = " + c.x); 
        c.method();
    }
}

class Parent { 
    int x = 100; // 같은 멤버 변수 int x를 정의하고 있다. 
    
    void method() {
        System.out.println("Parent Method");
    }
}

class Child extends Parent { 
    int x = 200; // 같은 멤버 변수 int x를 정의하고 있다. 

    void method() {
        System.out.println("Child Method");
    }
}
```

```
실행결과
p.x=100
Child Method
c.x=200
Child Method
```

7-21        
이 메서드의 매개변수로 가능한 것 두 가지?

```java
interface Movable {
    void move(int x, int y);
}
void attack(Movable f) {
        /*내용생략*/
}

```

```
1. null, 2. Movabal f
리턴타입이 인터페이스가 되는 것은, 
메소드가 해당 인터페이스를 구현한 클래스의 인스턴스를
반환한다는 의미이다. (매개변수의 다형성과 관련된 문제다.) p.388 
```

7-22        
도형을 정의한 shape 클래스를 조상으로 하는 Circle, Rectangle 클래스를 작성.       
(생성자도 적절하게 추가)

```
1. 
클래스명: Circle
조상클래스 : Shape 
멤버변수 : double r - 반지름
2.
클래스명: Rectangle 
조상클래스 : Shape
멤버변수 : double width - 폭 
        double height - 높이
메서드:       
  메서드명: isSquare
  기능: 정사각형인지 아닌지를 알려준다. 
  반환타입: boolean
  매개변수: 없음    
```

```java
abstract class Shape { 
    Point p;

    Shape() {
        this(new Point(0, 0));
    }
    
    Shape(Point p) {
        this.p = p;
    }
    
    abstract double calcArea; //  도형의 면적을 계산해서 반환하는 메서드

    Point getPosition() {
        return p;
    }
    void setPosition(Point p) {
        this.p = p;
    }
}

class Circle extends Shape { 
    double r;
    
    Circle(double r) {
        this(new Point(0,0),r); // Circle(Point p, double r) 호출
    }
    
    Circle(Point p, double r) {
        super(p);
        this.r = r;
    }
    double calcArea(){
        return Math.PI*r*r; // 원 넓이 구하기
    }
}

class Rectangle extends Shape{
    double width;
    double height;
    
    Rectangle(double width, double height) {
        this(new Point(0,0), width, height);
    }
    
    Rectangle(Point p, double width, double height){
        super(p);
        this.width = width;
        this.height = height;
    }
    
    boolean isSquare() { //정사각형은 각 변이 0이 아니면서, 길이가 같아야 함 
        if (!(width || height) == 0) && (width == height)
                return true;
    }
    double calcArea() {
        return width*height; // 정사각형 넓이 구하기
    }
}

class Point { 
    int x;
    int y; 
    Point() {
        this(0,0);
    }
    Point (int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    public String toString() {
        return "["+x+","+y+"]";
    }
}

```

7-23        
22문에서 정의한 클래스들의 면적을 구하는 메소드 작성

```
메서드명 : sumArea
기 능 : 주어진 배열에 담긴 도형들의 넓이를 모두 더해서 반환한다. 
반환타입 : double
매개변수 : Shape[] arr
```

```java
class Exercise7_23 {
    /*
            (1) sumArea메서드를 작성하시오.
     */
    static double sumArea(Shape[] arr){ //
        double sum = 0;
        
        for (int i=0; i < arr.length; i++)
            sum += arr[i].calcArea();
        return sum;
    }

    public static void main(String[] args){
        Shape[] arr = {new Circle(5.0), new Rectangle(3,4), new Circle(1)}; 
        System.out.println("면적의 합:"+sumArea(arr));
    }
}
```

7-24

```
다음 중 인터페이스의 장점이 아닌 것은?
a. 표준화를 가능하게 해준다.
b. 서로 관계없는 클래스들에게 관계를 맺어 줄 수 있다. 
c. 독립적인 프로그래밍이 가능하다.
d. 다중상속을 가능하게 해준다.
e. 패키지간의 연결을 도와준다.

e.

-기본 틀을 인터페이스로 만들고 이후 인터페이스의 구현체들을 생성하는 방식으로 표준화가 가능하다.
-서로 관계가 없는 클래스들이 같은 인터페이스를 구현하는 경우 관계를 맺을 수 있다.
-또한 인터페이스 사용으로 클래스의 선언과 구현체를 분리할 수 있기 때문에 구현 측면에서 독립적으로 프로그래밍할 수 있다. 
-인터페이스는 클래스 간 관계를 간접적으로 만들어 각 클래스가 독립적으로 코드 변경을 하더라도 다른 클래스에 영향을 미치지 않게 해준다. 
-단 하나의 조상 클래스를 상속받는 클래스와 달리, 인터페이스는 여러개를 다중 상속 받을 수 있다.
```

7-25        
Outer클래스의 내부 클래스 Inner의 멤버변수 iv의 값을 출력
```java
class Outer { //외부 클래스
    class Inner { //내부 클래스(인스턴스 클래스)
        int iv=100;
    }
}

class Exercise7_25 {
    public static void main(String[] args) {
        /*  
        (1) 알맞은 코드를 넣어 완성하시오.
        */
        Outer outer = new Outer(); // 먼저 외부 클래스의 인스턴스를 생성하고,
        Outer.Inner ii = outer.new Inner(); // 내부 클래스의 인스턴스를 생성한다.
        //인스턴스 클래스는 외부 클래스의 인스턴스가 생성되어야 사용가능.
        System.out.println(ii, iv);
    }
}
```
```
실행결과
100
```

7-26        
Outer클래스의 내부 클래스 Inner의 멤버변수 iv의 값을 출력

```java
class Outer { // 외부 클래스
    static class Inner { //내부 클래스, 
        //스태틱 클래스는 외부 클래스의 인스턴스를 생성하지 않아도 사용 가능하다. 
        int iv=200;
    }
}

class Exercise7_26 {
    public static void main(String[] args) {
         /*  
        (1) 알맞은 코드를 넣어 완성하시오.
        */
        Outer.inner ii = new Outer.Inner();
        System.out.println(ii,iv);
    }
}

```
```
실행결과
200
```

7-27        
실행결과를 얻도록 (1)~(4)의 코드를 완성

```java
class Outer {
    int value=10; //Outer.this.value

    class Inner { //인스턴스 클래스
        int value=20; //this.value
        void method1() {
            int value = 30; //value

            System.out.println(value);
            System.out.println(this.value);
            System.out.println(Outer.this.value;) // 외부 클래스의 인스턴스 변수는
            // 내부 클래스에서 '외부클래스 이름.this.변수이름'으로 접근 가능
        }
    } //Inner클래스의 끝
} // Outer클래스의 끝

class Exercise7_27 {
    public static void main(String args[]) {

        Outer outer = new Outer();
        Outer.inner innner = outer.new inner();

        inner.method1();
    }
}
```

```
실행결과
30 
20 
10
```

7-28        
EventHandler를 익명 클래스(anonymous class)로 변경
```java
import java.awt.*; 
import java.awt.event.*;

class Exercise7_28{

    public static void main(String[] args){

        Frame f = new Frame(); 
        // f.addWindowListener(new EventHandler());
        f.addWindowListener(new WindowAdapter(){
            public void windowClosing(WindowEvent e) {
                e.getWindow().setVisible(false);
                e.getWindow().dispose(); 
                System.exit(0);
            }
        }
        );
    } //main
}

// class EventHandler extends WindowAdapter { 
//     public void windowClosing(WindowEvent e) { 
//         e.getWindow().setVisible(false); 
//         e.getWindow().dispose(); 
//         System.exit(0);
//     }
// }
```

7-29        
지역 클래스에서 외부 클래스의 인스턴스 멤버와 static멤버에 모두 접근할 수 있지만,       
지역변수는 final이 붙은 상수만 접근할 수 있는 이유 무엇인가?

```
메소드가 수행을 마치고 지역변수가 소멸되어도 지역 클래스의 인스턴스가 소멸된 지역 변수를 참조하려는 경우가 발생할 수 있기 때문이다. p.407
final이 붙은 상수는 JVM constant pool에서 따로 관리하므로 생명주기가 달라지며, 메소드 안의 final 지역 변수는 메소드가 반납되어도 constant pool에 보관되어 있어 이를 참조하는 지역클래스의 인스턴스는 문제 없이 동작한다.
```



