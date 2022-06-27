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
        System.out.println(1);
        if (b) throw new ArithmeticException();
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

