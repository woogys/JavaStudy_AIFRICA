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
        return (int)(getTotal() / 3f * 10 * 0.5f) /10f;
    }
}
```
6-5     
실행 결과와 같도록 Student 클래스에 생성자 및 info() 추가
```java
class Exercise6_5 {
    public static void main(String args[]) {
        Student s = new Student("홍길동",1,1,100,60,76); 
        
        System.out.println(s.info());
    }
}
class Student {
    String name;
    int ban;
    int no;
    int kor;
    int eng;
    int math;
    
    Student(String name, int ban, int no, int kor, int eng, int math){
        this.name = name;
        this.ban = ban;
        this.kor = kor;
        this.eng = eng;
        this.math = math;
    }
    
    int getTotal(){
        return kor+eng+math;
    }
    
    float getAverage(){
        return (int)(getTotal() / 3f * 10 * 0.5f) /10f;
    }
    public String info(){
        retrun name
                +","+ban
                +","+no
                +","+kor
                +","+eng
                +","+math
                +","+getTotal()
                +","+getAverage()
        ;
    }
}
```

6-6     
두 점 거리 계산하는 메소드 getDistance() 완성
(제곱근 계산은 Math.sqrt(double a) 사용)
```java
class Exercise6_6 {
    static double getDistance(int x, int y, int x1, int y1){
        return Math.sqrt((x-x1)*(x-x1) + (y-y1)*y-y1); 
        // 두 점 사이 거리 공식은 루트 ((x-x1)^2 + (y-y1)^2)의 형태임
    }
    public static void main(String args[]) {
        System.out.println(getDistance(1,1,2,2));
    }
}
```
6-7     
6번 문제에서 작성한 클래스 메소드 getDistance()를 MyPoint 클래스 인스턴스 메소드로 정의
```java
class MyPoint {
    int x;
    int y;

    MyPoint(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    double getDistance(int x1, int y1){
        return Math.sqrt((x-x1)*(x-x1) + (y-y1)*y-y1);
    }
}
class Exercise6_7 {
    MyPoint p = new MyPoint(1,1);
            
    System.out.println.(p.getDistance(2,2));
}
```

6-8     
코드에 정의된 변수를 종류별로 구분해서 적으시오
```java
class PlayingCard{
    int kind;
    int num;
    
    static int width;
    static int height;
    
    PlayingCard(int k, int n){
        kind = k;
        num = n;
    }
    public static void main(String args[]){
        PlayingCard card = new PlayingCard(1,1);
    }
}
```
- 클래스 변수(static 변수) : width, height
- 인스턴스 변수 : kind, num 
- 지역 변수 : k,n, card, args

6-9     
클래스 멤버 중  static을 붙여야 하는 것은 어떤 것이고, 이유는?
(모든 병사의 공격력과 방어력은 같아야 함)
```java
class Marine{
    int x=0, y=0; // Marine의 위치 좌표(x,y)
    int hp = 60; // 현재 체력
    int weapon = 6; // 공격력
    int armor = 0 ; // 방어력
    
    void weaponUp(){
        weapon++;
    }
    
    void armorUp(){
        armor++;
    }
    
    void move(int x, int y){
        this.x = x;
        this.y = y;
    }
}
```
static int weapon = 6;      
static int armor = 0;       
static void weaponUp()      
static vodi armorUp()       

static은 모든 인스턴스에서 공통적인 값을 가져야 하는 변수다. 인스턴스 마린의 위치나 현재 체력은 고유의 각 개별 값이 있어야 한다.        
하지만 모든 병사의 공격력과 방어력은 같다고 문제에서 주어졌기 때문에 static을 붙여준다.        
메소드 weaponUp()과 armorUp()은 스태틱 변수인 weapon과 armor를 변경하는 것이므로 여기에도 붙여준다.

6-10
```
 다음 중 생성자에 대한 설명으로 옳지 않은 것은? (모두 고르시오) 
a. 모든 생성자의 이름은 클래스의 이름과 동일해야한다.
b. 생성자는 객체를 생성하기 위한 것이다.
c. 클래스에는 생성자가 반드시 하나 이상 있어야 한다.
d. 생성자가 없는 클래스는 컴파일러가 기본 생성자를 추가한다. 
e. 생성자는 오버로딩 할 수 없다.
```
b: 객체 생성은 new 연산자가 한다. 생성자는 객체를 초기화 하는 역할이다.        
e: 생성자도 오버로딩이 가능해서 하나의 클래스에 생성자 여러개를 정의해서 사용가능하다.

6-11
```
다음 중 this에 대한 설명으로 맞지 않은 것은? (모두 고르시오) 
a. 객체 자신을 가리키는 참조변수이다.
b. 클래스 내에서라면 어디서든 사용할 수 있다.
c. 지역변수와 인스턴스변수를 구별할 때 사용한다.
d. 클래스 메서드 내에서는 사용할 수 없다.
```
b: 클래스 멤버인 static이 붙은 변수나 메소드에는 사용할 수 없다.

6-12
```
다음 중 오버로딩이 성립하기 위한 조건이 아닌 것은? (모두 고르시오) 
a. 메서드의 이름이 같아야 한다.
b. 매개변수의 개수나 타입이 달라야 한다.
c. 리턴타입이 달라야 한다.
d. 매개변수의 이름이 달라야 한다.
```
c: 매개변수 개수나 타입만 다르면 된다. 
d: 매가변수 개수, 타입이 달라야 하지만 이름은 상관 없다.

6-13
```java
다음 중 아래의 add메서드를 올바르게 오버로딩 한 것은? (모두 고르시오) 

long add(int a, int b) { return a+b;}

a. long add(int x, int y) { return x+y;}
b. long add(long a, long b) { return a+b;}
c. int add(byte a, byte b) { return a+b;}
d. int add(long a, int b) { return (int)(a+b);}

```
b,c,d: 세 경우 모두 메소드 이름은 같으면서, 매개변수 타입이 다르기 때문에 오버로딩이 올바르게 되었다. (a는 매개변수 타입이 같음)

6-14
```
다음 중 초기화에 대한 설명으로 옳지 않은 것은? (모두 고르시오) 
a.멤버변수는 자동 초기화되므로 초기화하지 않고도 값을 참조할 수 있다. 
b.지역변수는 사용하기 전에 반드시 초기화해야 한다.
c.초기화 블럭보다 생성자가 먼저 수행된다.
d.명시적 초기화를 제일 우선적으로 고려해야 한다. 
e.클래스변수보다 인스턴스변수가 먼저 초기화된다.
```
c: 초기화 블럭이 수행된 이후에 생성자가 수행된다.       
e: 클래스변수는 클래스가 처음 메모리에 로딩되면 자동으로 초기화된다. 그 뒤에 인스턴스 변수가 초기화.

6-15

```
다음중 인스턴스변수의 초기화 순서가 올바른 것은? 
a. 기본값-명시적초기화-초기화블럭-생성자
b. 기본값-명시적초기화-생성자-초기화블럭
c. 기본값-초기화블럭-명시적초기화-생성자
d. 기본값-초기화블럭-생성자-명시적초기화
```
a: 인스턴스 변수는 인스턴스가 생성될 때마다 각 인스턴스별로 초기화 된다.     

6-16
```
다음 중 지역변수에 대한 설명으로 옳지 않은 것은? (모두 고르시오) 
a. 자동 초기화되므로 별도의 초기화가 필요없다.
b. 지역변수가 선언된 메서드가 종료되면 지역변수도 함께 소멸된다.
c. 매서드의 매개변수로 선언된 변수도 지역변수이다.
d. 클래스변수나 인스턴스변수보다 메모리 부담이 적다.
e. 힙(heap)영역에 생성되며 가비지 컬렉터에 의해 소멸된다.
```
a: 자동초기화되지 않기 때문에 사용 전 초기화를 반드시 진행해야 함.     
e: 힙은 인스턴스가 생성되는 영역이고, 지억변수는 call stack에 생성된다.


6-17
```
호출스택이 다음과 같은 상황일 때 옳지 않은 설명은? (모두 고르시오)
|println|
|-------|
|method1|
|-------|
|method2|
|-------|
|  main |

a. 제일 먼저 호출스택에 저장된 것은 main메서드이다.
b. println메서드를 제외한 나머지 메서드들은 모두 종료된 상태이다. 
c. method2메서드를 호출한 것은 main메서드이다.
d. println메서드가 종료되면 method1메서드가 수행을 재개한다.
e. main-method2-method1-println의 순서로 호출되었다.
f. 현재 실행중인 메서드는 println 뿐이다.
```
b: 스택은 아래에서 위로 쌓이므로 제일 위에 있는 println 메소드가 실행되고 있는 상태이고, 나머지는 대기 중이다.

6-18
다음 코드를 컴파일할 때 에러가 발생하는 라인과 이유 설명

```java
class MemberCall{
    int iv = 10;
    static int cv = 20;
    
    int iv2 = cv;
    static int cv2 = iv;   //라인 A
    
    static void staticMethod1(){
        System.out.println(cv);
        System.out.println(iv); // 라인 B
    }
    
    void instanceMethod1(){
        System.out.println(cv);
        System.out.println(iv); // 라인 C
    }
    
    static void staticMethod2(){
        staticMethod1();
        instanceMethod1(); // 라인 D
    }
    
    void instanceMethod2(){
        staticMethod1(); // 라인 E
        instanceMethod1();
    }
}
```
라인 A: static 변수를 초기화 할 때 인스턴스 변수를 사용할 수 없음      
라인 B: static메소드에서 인스턴스 변수 사용 불가
라인 D: static메소드에서 인스턴스 메소드 사용 불가

6-19 코드 실행 결과 예측

```java
class Exercise6_19 {
    public static void change(String str){
        str += "456";
    }
    
    public static void main(String args[]) {
        String str = "ABC123";
        System.out.println(str);
        chang(str);
        System.out.println("After Change:"+str);
    }
}
```
실행결과
```
ABC123
After change: ABC123
```
메소드 change 호출 후 참조 변수 str을 넘겨주면, 메소드 change의 지역 변수 str에 주소 값이 저장된다.     
그래서 change의 지역변수 str도 ABC123을 참조하게 된다.      
메소드 실행이 되면 문자열의 + 연산은 문자열에 합해지므로 ABC123456이 생성되긴 하나,         
메소드 종료 시 다시 메모리가 반환되면서 생성된 str안 ABC123456 역시 메모리에서 지워지게 되는 것.        

6-20        
문제의 정의에 따라 메소드 작성.
```
메서드명 : shuffle 
기 능 : 주어진 배열에 담긴 값의 위치를 바꾸는 작업을 반복하여 뒤섞이게 한다. 처리한 배열을 반환한다.
반환타입 : int[]
매개변수 : int[] arr - 정수값이 담긴 배열
```

```java
class Exercise6_20 {
    public static int[] shuffle(int[] arr){
        if(arr==null || arr.length==0) // 넘겨받을 값이 null이거나 크기가 0이면 그대로 반환 (유효성 체크 로직)
            return arr;
        
        for (int i=0; i<arr.length; i++){
            int j = (int)(Math.random()*arr.length);
            // arr[i], arr[j] 자리를 바꾸기 위해서 임시로 tmp 객체를 만들어 하나씩 밀어 자리바꿈. 
            int tmp = arr[i];
            arr[i] = arr[j];
            arr[j] = tmp;
        }
        return arr;
    }
    
    public static void main(String args[]) {
        int[] original = {1,2,3,4,5,6,7,8,9};
        System.out.println(java.util.Arrays.toString(original));
        
        int[] result = shuffle(original);
        System.out.println(java.util.Arrays.toString(result));
    }
}

```

6-21        
주어진 로직대로 tv 클래스 완성.

```java
class MyTv {
    boolean isPowerOn; 
    int channel; 
    int volume;

    final int MAX_VOLUME = 100; 
    final int MIN_VOLUME = 0; 
    final int MAX_CHANNEL = 100; 
    final int MIN_CHANNEL = 1;

    void turnOnOff() {
        // (1) isPowerOn의 값이 true면 false로, false면 true로 바꾼다.
        isPowerOn = !isPowerOn;
    }
    
    void volumeUp(){
            //(2) volume의 값이 MAX_VOLUME보다 작을 때만 값을 1증가시킨다.
        if (volume < MAX_VOLUME)
            volume++;
    }
    void volumeDown(){
        //(3) volume의 값이 MIN_VOLUME보다 클 때만 값을 1감소시킨다.
        if (volume>MIN_VOLUME)
            volume--;
    }
    void channelUp() {
        // (4) channel의 값을 1증가시킨다.
        // 만일 channel이 MAX_CHANNEL이면, channel의 값을 MIN_CHANNEL로 바꾼다.
        if (channel==MAX_CHANNEL){
            channel==MIN_CHANNEL;
        } else{
            channel++;
        }
    }

    void channelDown() {
        // (5) channel의 값을 1감소시킨다.
        // 만일 channel이 MIN_CHANNEL이면, channel의 값을 MAX_CHANNEL로 바꾼다.
        if (channel==MIN_CHANNEL){
            channel==MAX_CHANNEL;
        } else {
            channel--;
        }
    }
} // class MyTv

class Exercise6_21 {
    public static void main(String args[]) {
        MyTv t = new MyTv();
        
        t.channel = 100;
        t.volume = 0;
        System.out.println("CH:"+t.channel+", VOL:"+ t.volume);
        
        t.channelDown();
        t.volumeDown();
        System.out.println("CH:"+t.channel+", VOL:"+ t.volume);
        
        t.volume = 100;
        t.channelUp();
        t.volumeUp();
        System.out.println("CH:"+t.channel+", VOL:"+ t.volume);
    }
}
```

6-22        
정의된 메소드를 작성
```
메서드명 : isNumber
기 능 : 주어진 문자열이 모두 숫자로만 이루어져있는지 확인한다.
모두 숫자로만 이루어져 있으면 true를 반환하고,
그렇지 않으면 false를 반환한다.
만일 주어진 문자열이 null이거나 빈문자열“”이라면 false를 반환한다.
반환타입 :  boolean
매개변수 : String str - 검사할 문자열
```

```java
class Exercise6_22 {
    /*
    (1) isNumber메서드를 작성하시오.
     */
    public static boolean isNumber(String str){
        if(str==null || str.equals("")) //문자열이 null이거나 빈 문자열 ""이면 false
            return false;
        
        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i); // for문 돌려서 문자열에서 한글자식 읽어와서 변수명 ch에 담는다. 

            if (!('0'<=ch && ch <= '9')) { // 0부터 9까지의 숫자에 해당하지 않으면 false
                return false;
            }
        } 
        return true; //나머지 경우는 다 숫자이므로 true.
    }
    
    public static void main(String[] args) {
        String str = "123";
        System.out.println(str+"는 숫자입니까? "+isNumber(str));

        str = "1234o";
        System.out.println(str+"는 숫자입니까? "+isNumber(str));
    }
}
```

6-23        
정의된 메소드 완성
```
메서드명 : max 
기 능 : 주어진 int형 배열의 값 중에서 제일 큰 값을 반환한다.
만일 주어진 배열이 null이거나 크기가 0인 경우, -999999를 반환한다. 
반환타입 : int
매개변수 : int[] arr - 최대값을 구할 배열
```

```java
class Exercise6_23 {
/*
(1) max메서드를 작성하시오.
 */
    public static int max(int[] arr) {
        if (arr==null || arr.length==0) 
            return -999999; // arr이 null이거나 0일 때 반환해줄 값 
        
        int max = arr[0]; // max 값 초기화
        
        for (int i=1; i<arr.length; i++){ // 배열 값 안에서 비교해나가는 것이므로 배열 두번째 값부터 시작해서 처음 값과 비교해 나간다. 
            if(arr[i]>max) 
                max = arr[i];
         }
    }
    
public static void main(String[] args) {
    int[] data = {3,2,9,4,7}; 
    System.out.println(java.util.Arrays.toString(data)); 
    System.out.println("최대값:"+max(data)); 
    System.out.println("최대값:"+max(null)); 
    System.out.println("최대값:"+max(new int[]{})); // 크기가 0인 배열
 }
}

```

6-24        
정의된 메소드 완성
```
메서드명 : abs
기 능 : 주어진 값의 절대값을 반환한다.
반환타입 : int
매개변수 : int value
```
```java
class Exercise6_23 {
/*
(1) abs메서드를 작성하시오.
 */
    public static int abs(int value){
        return value >=0 ? value : -value; // 양수면 그냥 반환하면 되고 음수는 부호를 바꿔야 한다. 양수가 아니면(음수이면) value에 -가 붙기 때문에 결국 양수가 됨
    }

    public static void main(String[] args) {
        int value = 5;
        System.out.println(value + "의 절대값:" + abs(value));
        value = -10;
        System.out.println(value + "의 절대값:" + abs(value));
    }
}
```