14-1

```
메소드를 람다식으로 변환
```

```
int printVar(String name, int i) { 
    System.out.println(name+"="+i );
} 
(a) (name, i) -> System.out.println(name+"="+i )

int square(int x) {
    return x * x;
}
(b) (x) -> x * x

int roll() {
    return (int)(Math.random() * 6);
} 
(c) () -> (int)(Math.random() * 6)

int sumArr(int[] arr) { 
    int sum = 0;
    for(int i : arr) 
        sum += i;
    return sum;
}
(d) (int[] arr) -> { 
    int sum = 0;
    for(int i : arr) 
        sum += i;
    return sum;
}
매개변수의 타입이 있는 경우 ()괄호를 생략할 수 없다. 
{}괄호 안이 return문인 경우 괄호를 생략할 수 없다. 

int[] emptyArr() {
    return new int[]{};
}
(e) () -> new int[]{}

```


14-2

```
람다식을 메소드 참조 식으로 변환 (변환 불가시 '변환불가')
```

```
(String s) -> s.length()
String::length

()-> new int[]{}
int[]::new

arr -> Arrays.stream(arr)
Arrays::stream

(String str1, String str2) -> str1.equals(str2)
String::equals

(a, b) -> Integer.compare(a, b)
Integer::compare

(String kind, int num) -> new Card(kind, num)
Card::new

(x) -> System.out.println(x)
System.out::println

()-> Math.random()
Math::random

(str) -> str.toUpperCase()
String::toUpperCase

() -> new NullPointerException()
NullPointerException::new

(Optional opt) -> opt.get()
Optional::get

(StringBuffer sb, String s) -> sb.append(s)
StringBuffer::append

(String s) -> System.out.println(s)
System.out::println

```

14-3

```
아래의 괄호안에 알맞은 함수형 인터페이스는?
```

```java
( ) f; //함수형 인터페이스 타입의 참조변수 f를 선언.
 f = (int a, int b) -> a > b ? a : b;
```

```
a. Function
b. BiFunction
c. Predicate
d. IntBinaryOperator 
e. IntFunction

d.
매개변수와 반환값이 모두 int 타입이고, 매개변수가 둘이므로
이를 다룰 수 있는 IntBinaryOperator가 적절
(b는 binary이긴 하지만 int형을 사용 못함)
```

14-4

```
두 개의 주사위를 굴려서 나온 눈의 합이 6인 경우를 모두 출력 (배열 사용할 것)
```

```java
import java.util.*;
import java.util.stream.*;

class Exercise14_4 {
    public static void main(String[] args) {
        Stream<Integer> die = IntStream.rangeClosed(1, 6).boxed();
        //flatMap은 모든 element를 단일한 원소들의 스트림으로 반환해준다. 
        //중복 구조로 된 리스트를 하나의 스트림처럼 다룰 수 있다.
        //따라서 filter를 바로 체이닝해 사용가능.
        die.flatMap(i -> Stream.of(1, 2, 3, 4, 5, 6).map(i2 -> new int[]{i, i2}))
                .filter(iArr -> iArr[0] + iArr[1] == 6)
                .forEach(iArr -> System.out.println(Arrays.toString(iArr)));
    }
}
```

```
실행결과
[1, 5] 
[2, 4] 
[3, 3] 
[4, 2] 
[5, 1]
```

14-5

```
문자열 배열 strArr의 모든 문자열의 길이를 더한 결과를 출력

String[] strArr = { "aaa","bb","c", "dddd" };
```

```java
import java.util.stream.*;

class Exercise14_5 {
    public static void main(String[] args) {
        String[] strArr = {"aaa", "bb", "c", "dddd"};
        Stream<String> strStream = Stream.of(strArr);
        
        int sum = strStream.mapToInt(String::length).sum();
        System.out.println("sum=" + sum);
    }
}
```

```
실행결과
sum=10
```

14-6

```
문자열 배열 strArr의 문자열 중에서 가장 긴 것의 길이를 출력

String[] strArr = { "aaa","bb","c", "dddd" };
 
```

```java
import java.util.*;
import java.util.stream.*;

class Exercise14_5 {
    public static void main(String[] args) {
        String[] strArr = {"aaa", "bb", "c", "dddd"};
        Stream<String> strStream = Stream.of(strArr);

        strStream.map(String::length) // strStream.map(s-> s.length())
                .sorted(Comparator.reverseOrder()) // 문자열 길이로 역순 정렬
                .limit(1).forEach(System.out::println); // 제일 긴 문자열의 길이 출력
    }
}
```

```
실행결과
4
```

14-7

```
임의의 로또번호(1~45)를 정렬해서 출력
```

```java
import java.util.*;
import java.util.stream.*;

class Exercise14_6 {
    public static void main(String[] args) {
        new Random().ints(1, 46) // 1~45사이의 정수(46은 포함안됨)
                .distinct() // 중복제거
                .limit(6) // 6개만
                .sorted() // 정렬 
                .forEach(System.out::println); // 화면에 출력
    }
}
```

```
실행결과
2
3
4
13
42
43
```

14-8

```
불합격(150점 미만)한 학생의 수를 남자와 여자로 구별하여 출력하는 프로그램 완성
```

```java
import java.util.*;
import java.util.function.*;
import java.util.stream.*;

import static java.util.stream.Collectors.*;
import static java.util.Comparator.*;

class Student {
    String name;
    boolean isMale; // 성별 int hak; // 학년 int ban; // 반 int score;

    Student(String name, boolean isMale, int hak, int ban, int score) {
        this.name = name;
        this.isMale = isMale;
        this.hak = hak;
        this.ban = ban;
        this.score = score;
    }

    String getName() {
        return name;
    }

    boolean isMale() {
        return isMale;
    }

    int getHak() {
        return hak;
    }

    int getBan() {
        return ban;
    }

    int getScore() {
        return score;
    }

    public String toString() {
        return String.format("[%s, %s, %d학년 %d반, %3d점]", name, isMale ?
                "남" : "여", hak, ban, score);
    }

    // groupingBy()에서 사용
    enum Level {HIGH, MID, LOW} //성적을 상,중,하 세 단계로 분류
}

class Exercise14_8 {
    public static void main(String[] args) {
        Student[] stuArr = {
                new Student("나자바", true, 1, 1, 300),
                new Student("김지미", false, 1, 1, 250),
                new Student("김자바", true, 1, 1, 200),
                new Student("이지미", false, 1, 2, 150),
                new Student("남자바", true, 1, 2, 100),
                new Student("안지미", false, 1, 2, 50),
                new Student("황지미", false, 1, 3, 100),
                new Student("강지미", false, 1, 3, 150),
                new Student("이자바", true, 1, 3, 200),

                new Student("나자바", true, 2, 1, 300),
                new Student("김지미", false, 2, 1, 250),
                new Student("김자바", true, 2, 1, 200),
                new Student("이지미", false, 2, 2, 150),
                new Student("남자바", true, 2, 2, 100),
                new Student("안지미", false, 2, 2, 50),
                new Student("황지미", false, 2, 3, 100),
                new Student("강지미", false, 2, 3, 150),
                new Student("이자바", true, 2, 3, 200)
        };
        Map<Boolean, Map<Boolean, Long>> failedStuBySex =
                /*
                        (1) 알맞은 코드를 넣으시오.
                 */
        long failedMaleStuNum = failedStuBySex.get(true).get(true);
        long failedFemaleStuNum = failedStuBySex.get(false).get(true);

        System.out.println("불합격[남자]:" + failedMaleStuNum + "명");
        System.out.println("불합격[여자]:" + failedFemaleStuNum + "명");
    }
}
```

```
실행결과
불합격[남자]:2명 
불합격[여자]:4명
```

14-9

```
반별 총점을 학년 별로 나누어 출력하는 프로그램 완성
```

```java
import java.util.*;
import java.util.function.*;
import java.util.stream.*;
import static java.util.stream.Collectors.*;
import static java.util.Comparator.*;

class Student {
    String name;
    boolean isMale; // 성별 
    int hak; // 학년 
    int ban; // 반 
    int score;

    Student(String name, boolean isMale, int hak, int ban, int score) {
        this.name = name;
        this.isMale = isMale;
        this.hak = hak;
        this.ban = ban;
        this.score = score;
    }

    String getName() {
        return name;
    }

    boolean isMale() {
        return isMale;
    }

    int getHak() {
        return hak;
    }

    int getBan() {
        return ban;
    }

    int getScore() {
        return score;
    }

    public String toString() {
        return String.format("[%s, %s, %d학년 %d반, %3d점]", name, isMale ? "남" : "여", hak, ban, score);
    }

    enum Level {HIGH, MID, LOW}
}

class Exercise14_9 {
    public static void main(String[] args) {
        Student[] stuArr = {
                new Student("나자바", true, 1, 1, 300),
                new Student("김지미", false, 1, 1, 250),
                new Student("김자바", true, 1, 1, 200),
                new Student("이지미", false, 1, 2, 150),
                new Student("남자바", true, 1, 2, 100),
                new Student("안지미", false, 1, 2, 50),
                new Student("황지미", false, 1, 3, 100),
                new Student("강지미", false, 1, 3, 150),
                new Student("이자바", true, 1, 3, 200),

                new Student("나자바", true, 2, 1, 300),
                new Student("김지미", false, 2, 1, 250),
                new Student("김자바", true, 2, 1, 200),
                new Student("이지미", false, 2, 2, 150),
                new Student("남자바", true, 2, 2, 100),
                new Student("안지미", false, 2, 2, 50),
                new Student("황지미", false, 2, 3, 100),
                new Student("강지미", false, 2, 3, 150),
                new Student("이자바", true, 2, 3, 200)
        };
        
        Map<Integer, Map<Integer, Long>> totalScoreByHakAndBan =
                        /*
                        (1) 알맞은 코드를 넣으시오.
                 */

        for (Object e : totalScoreByHakAndBan.entrySet()) {
            System.out.println(e);
        }
    } //main의끝
}
```

```
실행결과
1={1=750, 2=300, 3=450} 
2={1=750, 2=300, 3=450}
```