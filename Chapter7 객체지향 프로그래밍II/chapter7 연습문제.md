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

