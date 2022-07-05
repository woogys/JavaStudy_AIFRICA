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
        cal.set(2010,0,1); // 2010년 1월 1일로 초기화, 월은 0부터 인덱싱
        
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
import sun.util.resources.cldr.ar.CalendarData_ar_AE;

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
        if (from == null || to == null) {
            return 0; //from 또는 to가 null이면 0을 반환한다.
        }
        if (from.equals(to) && from.get(Calendar.DAY_OF_MONTH) == 21) {
            return 1; // from와 to가 같고 날짜가 21일이면 1을 반환한다.
        }
        
        int fromYear = from.get(Calendar.YEAR);
        int fromMonth = from.get(Calendar.MONTH);
        int fromDay = from.get(Calendar.DAY_OF_MONTH);

        int toYear = to.get(Calendar.YEAR);
        int toMonth = to.get(Calendar.MONTH);
        int toDay = to.get(Calendar.DAY_OF_MONTH);
        
        int monDiff = (toYear * 12 + toMonth) - (fromYear * 12 + fromMonth); 
        // to와 from이 몇 개월 차이인지 계산해서 변수 monDiff에 담는다.

        if (monDiff < 0 ) {
            return 0; //monDiff가 음수이면 0을 반환한다.
        }
        
        if (fromDay <= 21 && toDay >= 21){
            return monDiff++; //만일 from의 일(DAY_OF_MONTH)이 21일이거나 이전이고
                             // to의 일(DAY_OF_MONTH)이 21일이거나 이후이면 monDiff의 값을 1 증가시킨다.
        }
        
        if (fromDay > 21 && toDay < 21) {
            monDiff--;   //만일 from의 일(DAY_OF_MONTH)이 21일 이후고
                        //to의 일(DAY_OF_MONTH)이 21일 이전이면 monDiff의 값을 1 감소시킨다.
        }

        return monDiff;
    }

    static void printResult(Calendar from, Calendar to) {
        Date fromDate = from.getTime();
        Date toDate = to.getTime();

        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        System.out.print(sdf.format(fromDate) + " ~ "
                + sdf.format(toDate) + ":");
        System.out.println(paycheckCount(from, to));
    }

    public static void main(String[] args) {
        Calendar fromCal = Calendar.getInstance();
        Calendar toCal = Calendar.getInstance();
        fromCal.set(2010, 0, 1);
        toCal.set(2010, 0, 1);
        printResult(fromCal, toCal);

        fromCal.set(2010, 0, 21);
        toCal.set(2010, 0, 21);
        printResult(fromCal, toCal);

        fromCal.set(2010, 0, 1);
        toCal.set(2010, 2, 1);
        printResult(fromCal, toCal);

        fromCal.set(2010, 0, 1);
        toCal.set(2010, 2, 23);
        printResult(fromCal, toCal);

        fromCal.set(2010, 0, 23);
        toCal.set(2010, 2, 21);
        printResult(fromCal, toCal);

        fromCal.set(2011, 0, 22);
        toCal.set(2010, 2, 21);
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
10-3

```
문자열 “123,456,789.5”를 소수점 첫 번째 자리에서 반올림하고, 그 값을 만 단 위마다 콤마(,)로 구분해서 출력
```

```java
import java.text.*;
class Exercise10_3{
    public static void main(String[] args){
        String data = "123,456,789.5";

        DecimalFormat df = new DecimalFormat("#,###.##"); // 변환할 문자열의 형식을 지정 
        DecimalFormat df2 = new DecimalFormat("#,####");

        try {
            Number num = df.parse(data);
            
            double d = num.doubleValue(); 
            System.out.println("data:"+data); 
            System.out.println("반올림:"+Math.round(d)); 
            System.out.println("만단위:"+df2.format(d));
        } catch(Exception e) {} 
    }  // main
}
    
```

```
실행결과
data:123,456,789.5 
반올림:123456790 
만단위:1,2345,6790

특정 형식의 문자열을 숫자로 변환하려면 DecimalFormat 클래스에 형식을 정의하고, parse()를 이용한다.
반환 타입은 Number이므로, 다시 doubleValue()를 호출해서 double 타입으로 값을 얻어야 한다.
```

10-4

```
날짜를 “2007/05/11”의 형태로 입력받아서 무슨 요일인지 출력
입력 날짜 형식이 잘못된 경우 메세지를 보여주고 다시 입력받음
```

```java
import java.util.*; 
import java.text.*;

class Exercise10_4 {
    public static void main(String[] args) {
        String pattern = "yyyy/MM/dd"; 
        String pattern2 = "입력하신 날짜는 E요일입니다."; // 'E'는 일~토 중의 하나가 된다.

        DateFormat df = new SimpleDateFormat(pattern); //  SimpleDateFormat은 날찌를 지정된 형식으로 출력하거나,
        DateFormat df2 = new SimpleDateFormat(pattern2); // 문자열을 지정된 형식으로 변환해준다. (유효성 검사에도 이용 가능)
        
        Scanner sc = new Scanner(System.in);

        Date inDate = null;
        
        do { 
            System.out.println("날짜를 " + pattern
                + "의 형태로 입력해주세요.(입력예:2007/05/11)");
            try {
                System.out.print(">>");
                inDate = df.parse(sc.nextLine()); // 입력받은 날짜를 Date로 변환한다. 지정된 형식과 다를 경우,
                break; // parse()에서 예외가 발생(ParseException이 발생할 수 있다.)하고 이 부분은 수행되지 않는다. 
                } catch(Exception e) {}
            } while(true);
            System.out.println(df2.format(inDate));
    } //main
}
```

```
실행결과
날짜를 yyyy/MM/dd의 형태로 입력해주세요.(입력예:2007/05/11) 
>>2009-12-12
날짜를 yyyy/MM/dd의 형태로 입력해주세요.(입력예:2007/05/11)
>>2009/12/12
입력하신 날짜는 토요일입니다.
```

10-5
```
다음 조건에 따라 메소드 작성

메서드명 : getDayDiff
기 능 : yyyymmdd형식의 두 문자열을 넘겨받으면 두 날짜의 차이를 일(day)단위로 반환한다. 
       단, 첫 번째 날짜 빼기 두 번째 날짜의 결과를 반환한다.
       만일 주어진 문자열이 유효하지 않으면 0을 반환한다.
반환타입 : int
매개변수 : String yyyymmdd1 - 시작날짜
         String yyyymmdd2 - 끝 날짜
```

```java
import java.util.*;
class Exercise10_5 {
    /* 
    (1) getDayDiff메서드를 작성하시오. 
    */
    static int getDayDiff (String yyyymmdd1, String yyyymmdd2) {
        int diff = 0;
        
        try {
            int year1 = Integer.parseInt(yyyymmdd1.substring(0,4));
            int month1 = Integer.parseInt(yyyymmdd1.substring(4,6)) - 1; // month는 0~11 이므로 -1 해줘야 맞게 나온다. 
            int day1 = Integer.parseInt(yyyymmdd1.substring(6,8));
            
            int year2 = Integer.parseInt(yyyymmdd2.substring(0,4));
            int month2 = Integer.parseInt(yyyymmdd2.substring(4,6)) - 1;
            int day2 = Integer.parseInt(yyyymmdd2.substring(6,8));
            
            Calendar date1 = Calendar.getInstance();
            Calendar date2 = Calendar.getInstance();
            
            date1.set(year1, month1, day1);
            date2.set(year2, month2, day2);
            
            diff = (int) ((date1.getTimeInMillis()-date2.getTimeInMillis())/(24*60*60*1000));
            // getTimeInMillis는 날짜를 천분의 일초로 변환해준다. 변환된 두 날짜간 차이를 구한 뒤 일 단위로 다시 변환하면
            //날짜 차이를 구할 수 있다. 천분의 일초 단위를 바꾸려면 /(24*60*60*1000)로 나눈다. 
        } catch (Exception e) {
            diff = 0; // 예외 발생시 0 리턴
        }
        return diff;
    }
    public static void main(String[] args){ 
        System.out.println(getDayDiff("20010103","20010101")); 
        System.out.println(getDayDiff("20010103","20010103")); 
        System.out.println(getDayDiff("20010103","200103"));
    }
}
```

```
실행결과
2
0
0
```

10-6

```
자신이 태어난 날로부터 지금까지 며칠이 지났는지 계산, 출력
```

```java
import java.time.*;
import java.time.temporal.*;

class Exercise10_6 {
    public static void main(String[] args) {
        LocalDate birthDay = LocalDate.of(1989, 6, 11); 
        LocalDate now = LocalDate.now();

        long days = birthDay.until(now, ChronoUnit.DAYS); // LocalDate의 until() 사용

        System.out.println("birth day="+birthDay); 
        System.out.println("today ="+now); 
        System.out.println(days +" days");
    }
}
```

```
birth day=1989-06-11 
today =2022-07-05 
12077 days
```

10-7

```
2016년 12월 네번째 화요일의 날짜를 아래의 실행결과와 같은 형식으로 출력
```

```java
import java.time.*;
import static java.time.DayOfWeek.*;
import static java.time.temporal.TemporalAdjusters.*;

class Exercise10_7 {
    public static void main(String[] args) {
        LocalDate date = LocalDate.of(2016, 12, 1);
        System.out.println(date.with(dayOfWeekInMonth(4, TUESDAY))); // x째 주 x요일은 dayOfWeekInMonth 사용
    }
}
```

```
실행결과
2016-12-27
```

10-8

```
서울과 뉴욕간의 시차가 얼마인지 계산
```

```java
import java.time.*;

class Exercise10_8 {
    public static void main(String[] args) {
        ZonedDateTime zdt = ZonedDateTime.now(); 
        ZoneId nyId = ZoneId.of("America/New_York");
        ZonedDateTime zdtNY = ZonedDateTime.now().withZoneSameInstant(nyId);

        System.out.println(zdt); 
        System.out.println(zdtNY);

        long sec1 = zdt.getOffset().getTotalSeconds();  // getOffSet은 ZoneOffSet 반환.
        long sec2 = zdtNY.getOffset().getTotalSeconds(); // ZoneOffSet의 getTotalSeconds()를 호출하면 
        long diff = (sec1 - sec2)/3600; // 날짜와 초단위로 변환한 결과가 나옴, 이를 다시 3600(60*60)으로 나눠 일 수로 변환 

        System.out.println("sec1="+sec1); 
        System.out.println("sec2="+sec2); 
        System.out.printf("diff=%d hrs%n",diff);
    }
}
```

```
실행결과
2022-07-05T23:13:29.037+09:00[Asia/Seoul]
2022-07-05T10:13:40.685-04:00[America/New_York]
sec1=32400
sec2=-14400
diff=13 hrs
```
