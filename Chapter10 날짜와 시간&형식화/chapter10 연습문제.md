10-1
```
Calendar클래스와 SimpleDateFormat클래스를 이용,
2010년의 매월 두 번째 일요일 날짜 출력
```

```java
import java.util.*; 
import java.text.*;

class Exercise10_1 {
    public static void main(String[] args) {
        Calendar cal = Calendar.getInstance(); 
        // 추상클래스 Calendar는 메소드를 통해 완전히 구현된 클래스의 인스턴스를 얻는다.
        cal.set(2010,0,1); // 2010년 1월 1일로 초기화, 월은 0부터 인덱스 시
        
        for (int i = 0; i < 12; i++) {
            int weekday = cal.get(Calendar.DAY_OF_WEEK); // 1일이 무슨 요일인지 구한다.
            int secondSunday = (weekday == 1) ? 8 : 16 - weekday;
            // 두 번째 일요일은 1일이 일요일이면 8일이고, 다른 요일이면 16일-1일 요일을 빼면 나옴
            // 16은 2주뒤 - 해당 요일을 하면 일요일로 감
            cal.set(Calendar.DAY_OF_MONTH, secondSunday); // 두 번째 일요일로 cal의 날짜를 바꾼다.
            Date d = cal.getTime();
            System.out.println(new SimpleDateFormat("yyyy-MM-dd은 F 번째 E요일입니다.").format(d));
        
            cal.add(Calendar.MONTH, 1);
            cal.set(Calendar.DAY_OF_MONTH, 1);
        }
    }
}

```
```
실행결과
2010-01-10은 2번째 일요일입니다. 
2010-02-14은 2번째 일요일입니다. 
2010-03-14은 2번째 일요일입니다. 
2010-04-11은 2번째 일요일입니다. 
2010-05-09은 2번째 일요일입니다. 
2010-06-13은 2번째 일요일입니다. 
2010-07-11은 2번째 일요일입니다. 
2010-08-08은 2번째 일요일입니다. 
2010-09-12은 2번째 일요일입니다. 
2010-10-10은 2번째 일요일입니다. 
2010-11-14은 2번째 일요일입니다. 
2010-12-12은 2번째 일요일입니다.
```

10-2
```
어떤 회사 월급날은 21일. 두 날짜 사이에 월급날이 몇 번 있는지
계산, 반환하는 메소드 작
```

```java
import java.util.*; 
import java.text.*;

class Exercise10_2 {
    static int paycheckCount(Calendar from, Calendar to) {
        /*
        (1) 아래의 로직에 맞게 코드를 작성하시오.
         1. from 또는 to가 null이면 0을 반환한다.
         2. from와 to가 같고 날짜가 21일이면 1을 반환한다.
         3. to와 from이 몇 개월 차이인지 계산해서 변수 monDiff에 담는다. 
         4. monDiff가 음수이면 0을 반환한다.
         5. 만일 from의 일(DAY_OF_MONTH)이 21일이거나 이전이고
            to의 일(DAY_OF_MONTH)이 21일이거나 이후이면 monDiff의 값을 1 증가시킨다. 
         6. 만일 from의 일(DAY_OF_MONTH)이 21일 이후고
            to의 일(DAY_OF_MONTH)이 21일 이전이면 monDiff의 값을 1 감소시킨다.
         */
        return monDiff;
    }

    static void printResult(Calendar from, Calendar to) {
        Date fromDate = from.getTime();
        Date toDate = to.getTime();
        
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        System.out.print(sdf.format(fromDate)+" ~ "
                +sdf.format(toDate)+":");
        System.out.println(paycheckCount(from, to));
    }

    public static void main(String[] args) {
        Calendar fromCal = Calendar.getInstance(); 
        Calendar toCal = Calendar.getInstance();
        fromCal.set(2010,0,1); 
        toCal.set(2010,0,1); 
        printResult(fromCal, toCal);
        
        fromCal.set(2010,0,21); 
        toCal.set(2010,0,21); 
        printResult(fromCal, toCal);
        
        fromCal.set(2010,0,1); 
        toCal.set(2010,2,1); 
        printResult(fromCal, toCal);
        
        fromCal.set(2010,0,1); 
        toCal.set(2010,2,23); 
        printResult(fromCal, toCal);
        
        fromCal.set(2010,0,23); 
        toCal.set(2010,2,21); 
        printResult(fromCal, toCal);
        
        fromCal.set(2011,0,22); 
        toCal.set(2010,2,21); 
        printResult(fromCal, toCal);
    }
}

```

```
실행결과
2010-01-01 ~ 2010-01-01:0 
2010-01-21 ~ 2010-01-21:1 
2010-01-01 ~ 2010-03-01:2 
2010-01-01 ~ 2010-03-23:3 
2010-01-23 ~ 2010-03-21:2 
2011-01-22 ~ 2010-03-21:0
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
