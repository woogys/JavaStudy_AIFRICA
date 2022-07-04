8-1
```
Q.예외 처리의 정의와 목적?

A.
  정의: 예외처리는 프로그램을 실행할 때 발생할 수 있는 예외를 대비해 코드를 작성하는 것이다.
  목적: 예기치 못한 예외로 인해 프로그램이 비정상적으로 종료되는 것을 막는 것이다. 
```

8-2
```
다음은 실행 도중 예외가 발생하여 화면에 출력된 내용이다. 옳지 않은 것은?
```
```bash
java.lang.ArithmeticException : / by zero 
        at ExceptionEx18.method2(ExceptionEx18.java:12) 
        at ExceptionEx18.method1(ExceptionEx18.java:8) 
        at ExceptionEx18.main(ExceptionEx18.java:4)
```
```
a. 위의 내용으로 예외가 발생했을 당시 호출스택에 존재했던 메서드를 알 수 있다.
b. 예외가 발생한 위치는 method2 메서드이며, ExceptionEx18.java파일의 12번째 줄이다. 
c. 발생한 예외는 ArithmeticException이며, 0으로 나누어서 예외가 발생했다.
d. method2메서드가 method1메서드를 호출하였고 그 위치는 ExceptionEx18.java파일의 8 번째 줄이다.

d.
스택 트레이스는 아래에서 위로 읽어야 하므로 method1이 method2를 호출한 것이다.
```

8-3
```
다음 중 오버라이딩이 잘못된 것을 모두 골라라.
```
```java
void add(int a, int b)
    throws InvalidNumberException, NotANumberException {}

class NumberException extends Exception {}
class InvalidNumberException extends NumberException {} 
class NotANumberException extends NumberException {}
```
```
a. void add(int a, int b) throws InvalidNumberException, NotANumberException {} 
b. void add(int a, int b) throws InvalidNumberException {}
c. void add(int a, int b) throws NotANumberException {}
d. void add(int a, int b) throws Exception {}
e. void add(int a, int b) throws NumberException {}

        Exception
            ↑
      NumberException
      ↑            ↑
 InvalidEx     NotANumberEx     

오버라이딩은 부모 클래스에 있는 메소드를 자식 클래스에서 재정의해 사용하는 것이다. 
메소드 이름이 같고, 파라미터가 같고, 리턴 타입이 같다. 부모 클래스의 메소드보다 더 큰 범위의 예외는 선언할 수 없다.
 
d.
Exception은 최상위 클래스이므로 예외의 범위가 더 크다. 따라서 오버라이딩 원칙에 위배된다.

e.
InvalidNumber, NotANumber는 모두  NumberException을 상속받고 있다. 따라서 잘못되었다.
```

8-4
```
다음 같은 메소드가 있을 때, 예외처리가 잘못된 곳을 모두 골라라
```
```java
void method() throws InvalidNumberException, NotANumberException {}

class NumberException extends RuntimeException {}
class InvalidNumberException extends NumberException {} 
class NotANumberException extends NumberException {}
```

```
a. try {method();} catch(Exception e) {}
b. try {method();} catch(NumberException e) {} catch(Exception e) {} 
c. try {method();} catch(Exception e) {} catch(NumberException e) {} 
d. try {method();} catch(InvalidNumberException e) {} catch(NotANumberException e) {} 
e. try {method();} catch(NumberException e) {}
f. try {method();} catch(RuntimeException e) {}

        RuntimeException
               ↑
        NumberException
       ↑                ↑
  InvalidNumber     NotANumber

c. Exception은 최상위 클래스이므로 가장 마지막 catch 블럭에 있어야 한다. c는 그렇지 않다. 

```

8-5
```
아래 코드가 실행될 때 결과를 적으시오.
```
```java
class Exercise8_5 {
static void method(boolean b) {
    try {
        System.out.println(1); // 1출력
        if (b) throw new ArithmeticException(); // true니까 예외 발생 
        System.out.println(2);
    } catch (RuntimeException r) {
        System.out.println(3);
        return;
    } catch (Exception e) {
        System.out.println(4);
        return;
    } finally {
        System.out.println(5);
    }
    System.out.println(6);
}
    public static void main(String[] args) { 
    method(true);
    method(false); 
    } // main
}
```
```
실행결과
1
3
5
1
2
5
6
103/ 1 출력 -> 104/true니까 예외 발생 -> 첫번째 catch 3 출력 -> finally는 예외 관계없이 실행, 5출력
-> 첫번째 catch 리턴에서 method(false) 실행 -> 1출력 -> false니까 2출력 -> finally, 5 출력 -> 6 출력  

```

8-6
```
아래 코드가 실행될 때 결과를 적으시오.
```
```java
class Exercise8_6 {
    public static void main(String[] args) {
        try {
            method1();
        } catch (Exception e) {
            System.out.println(5);
        }
    }


    static void method1() {
        try {
            method2(); 
            System.out.println(1);
        } catch(ArithmeticException e) { 
            System.out.println(2);
        } finally {
            System.out.println(3);
        }
        
        System.out.println(4); 
    } // method1()
    static void method2() {
        throw new NullPointerException();
    }
}
```
```
실행결과
3
5

method1() -> method2(), NPE 발생 but try-catch로 해결 불가하므로 종료
-> method1()에서도 처리 불가 -> finally로 3이 찍히고 main메소드로 돌아감
-> 메인 메소드에서 예외처리 후 5 출력  
```

8-7
```
아래 코드가 실행될 때 결과를 적으시오.
```
```java
class Exercise8_7 {
static void method(boolean b) {
    try {
        System.out.println(1); 
        if(b) System.exit(0); //괄호 안 0은 정상 종료, 1이 있으면 비정상 종료
        System.out.println(2);
    } catch(RuntimeException r) { 
        System.out.println(3); 
        return;
    } catch(Exception e) { 
        System.out.println(4); 
        return;
    } finally {
        System.out.println(5); }
    System.out.println(6);
}

    public static void main(String[] args) { 
        method(true);
        method(false); 
    } // main
}
```
```
실행결과
1

b가 true이므로 System.exit이 일어나 1만 출력되고 프로그램이 종료됨
```

8-8
```
다음은 1~100 사이 숫자를 맞추는 게임이 실행되던 중 영문자를 넣어 발생한 예외다.
예외처리를 해서 숫자 아닌 값이 입력되면 다시 입력받도록 만들기
```
```bash
1과 100사이의 값을 입력하세요 :50
더 작은 수를 입력하세요.
1과 100사이의 값을 입력하세요 :asdf
Exception in thread "main" java.util.InputMismatchException
    at java.util.Scanner.throwFor(Scanner.java:819) 
    at java.util.Scanner.next(Scanner.java:1431)
    at java.util.Scanner.nextInt(Scanner.java:2040) 
    at java.util.Scanner.nextInt(Scanner.java:2000) 
    at Exercise8_8.main(Exercise8_8.java:16)
```
```java
import java.util.*; class Exercise8_8{

public static void main(String[] args) {
    // 1~100사이의 임의의 값을 얻어서 answer에 저장한다. 
    int answer = (int)(Math.random() * 100) + 1; 
    int input = 0; // 사용자입력을 저장할 공간 
    int count = 0; //시도횟수를 세기 위한 변수
    
    do {
        count++;
        System.out.print("1과 100사이의 값을 입력하세요 :");
        input = new Scanner(System.in).nextInt();
        
        try {
            input = new Scanner(System.in).nextInt(); 
        } catch (Exception e) {
            System.out.println("유효하지 않은 값입니다." + " 다시 입력해주세요.");
            continue;
        }

        if(answer > input) {
            System.out.println("더 큰 수를 입력하세요.");
        } else if(answer < input) { 
            System.out.println("더 작은 수를 입력하세요.");
        } else {
            System.out.println("맞췄습니다."); 
            System.out.println("시도횟수는 "+count+"번입니다."); 
            break; // do-while문을 벗어난다
        }
      } while(true); // 무한반복문
    } // end of main
} // end of class HighLow
```
8-9
```
다음과 같은 조건의 예외 클래스를 작성하라.
(생성자는 실행 결과를 보고 알맞게 작성)

* 클래스명 : UnsupportedFuctionException 
* 조상클래스명 : RuntimeException
* 멤버변수 :
    이 름 : ERR_CODE 
    저장값 : 에러코드
    타 입 : int
    기본값 : 100
    제어자 : final private
* 메서드 :
 1. 
  메서드명 : getErrorCode
  기 능 : 에러코드(ERR_CODE)를 반환한다.
  반환타입 : int
  매개변수 : 없음
  제어자 : public
       
 2. 
  메서드명 : getMessage
  기 능 : 메세지의 내용을 반환한다.(Exception클래스의 getMessage()를 오버라이딩)
  반환타입  : String
  매개변수: 없음
  제어자: public
```

```java
class UnsupportedFunctionException extends RuntimeException {
    private final int ERR_CODE;
    
    UnsupportedOperationException(String msg, int errCode) { //생성자
        super(msg); //RuntimeException(String msg)를 호출
        ERR_CODE = errCode;
    }
    
    UnsupportedOperationException(String msg) {
        this(msg, 100); //에러코드는 기본값 100
    }
    
    public int getErrorCode() { //에러코드를 반환한다.
        return ERR_CODE; 
    }
    
    public String getMessage() { // 메세지의 내용을 반환한다.(Exception클래스의 getMessage()를 오버라이딩)
        return "[" + getERR_CODE() +"]" + super.getMessage();
    }
}

class Exercise8_9 { 
    public static void main(String[] args) throws Exception {
        throw new UnsupportedFuctionException("지원하지 않는 기능입니다.",100);
    }
}
```

```bash
실행결과
Exception in thread "main" UnsupportedFuctionException: [100]지원하지 않는 기능 입니다. 
  at Exercise8_9.main(Exercise8_9.java:5)
```

8-10
```
아래 코드가 실행되었을 때의 결과?
```
```java
class Exercise8_10 {
    public static void main(String[] args) {
        try {
            method1();
            System.out.println(6);
        } catch (Exception e) {
            System.out.println(7);
        }
    }

    static void method1() throws Exception {
        try {
            method2();
            System.out.println(1);
        } catch (NullPointerException e) {
            System.out.println(2);
            throw e;
        } catch (Exception e) {
            System.out.println(3);
        } finally {
            System.out.println(4);
        }
        System.out.println(5);
    } // method1()

    static void method2() {
        throw new NullPointerException();
    }
}
```

```
실행결과
2
4
7

method1() -> method2(), NPE -> method1()의 첫번째 catch에서 NPE 처리, 2 출력
-> throw e; 로 예외 되던지기 발생, finally 실행으로 4 출력 -> 메인함수 catch에서 
예외 처리 후 7 출력 되고 try-catch 벗어나 종료
```
