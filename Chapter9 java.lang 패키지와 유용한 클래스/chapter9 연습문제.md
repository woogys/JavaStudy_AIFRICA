9-1
```
SutdaCard 클래스의 equals()를 멤버변수인 num, isKwang의
값을 비교하도록 오버라이딩해 실행 결과가 나오도록 완성
```

```java
class Exercise9_1 {
public static void main(String[] args) {
    SutdaCard c1 = new SutdaCard(3, true);
    SutdaCard c2 = new SutdaCard(3, true);

    System.out.println("c1=" + c1);
    System.out.println("c2=" + c2);
    System.out.println("c1.equals(c2):" + c1.equals(c2));
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

    public boolean equals(Object obj) { //Object 타입은 어떤 타입의 인스턴스든지 매개변수로 받을 수 있음
    /* 
        (1) 매개변수로 넘겨진 객체의 num, isKwang과
            멤버변수 num, isKwang을 비교하도록 오버라이딩 하시오.
    */
        if(obj instanceof SutdaCard) { // 따라서 instanceof 연산자로 타입을 확인 후 형변환 해야 함
            SutdaCard c = (SutdaCard) obj;  // 
            return num == c.num && isKwang == c.isKwang;
        }
        return false;
    }

    public String toString() {
        return num + (isKwang ? "K" : "");
    }
}
```

```bash
실행결과
c1=3K
c2=3K
c1.equals(c2):true
```

9-2
```
실행결과를 얻도록 Point3D클래스의 equals()를 
멤버변수인 x, y, z 의 값을 비교하도록 오버라이딩하고,
toString()은 실행결과를 참고해서 적절히 오버라이딩
```

```java
class Exercise9_2 {
public static void main(String[] args) {
    Point3D p1 = new Point3D(1, 2, 3);
    Point3D p2 = new Point3D(1, 2, 3);

    System.out.println(p1);
    System.out.println(p2);
    System.out.println("p1==p2?" + (p1 == p2));
    System.out.println("p1.equals(p2)?" + (p1.equals(p2)));
    }
}

class Point3D { int x,y,z;
    Point3D(int x, int y, int z) { this.x=x;
        this.y=y;
        this.z=z;
    }

    Point3D() {
        this(0, 0, 0);
    }
    public boolean equals(Object obj) {
        /* 
        (1) 인스턴스변수 x, y, z를 비교하도록 오버라이딩하시오.
         */
        if (obj instanceof Point3D){
            Point3D p = (Point3d) obj;
            return x == p.x && y == p.y && z == p.z;
        }
        return false;
    }
    public String toString() {
        /* 
        (2) 인스턴스변수 x, y, z의 내용을 출력하도록 오버라이딩하시오.
         */
        return "["+x+","+y+","+z+"]";
    }
}
    
```
```bash
[1,2,3]
[1,2,3]
p1==p2?false
p1.equals(p2)?true
```

9-3
```
실행결과가 나오도록 코드 완성
```

```java
class Exercise9_3 {
    public static void main(String[] args) {
        String fullPath = "c:\\jdk1.8\\work\\PathSeparateTest.java";
        String path = "";
        String fileName = "";
    
      /* 
      (1) 알맞은 코드를 넣어 완성하시오.
       */
        int pos = fullPath.lastIndexOf("\\"); // 마지막 경로 부분을 잘라야 하므로 lastIndexOf() 사용 p.470
        
        if(pos != -1){ // lastIndexOf는 만약 못찾으면 -1을 반환하므로, 그 경우에 대비한다.  
            path = fullPath.substring(0, pos); // 0 <= path <pos
            fileName = fullPath.substring(pos+1); // 지정된 위치부터 끝까지 자름 p.470
        }
        
        System.out.println("fullPath:" + fullPath);
        System.out.println("path:" + path);
        System.out.println("fileName:" + fileName);
    }
}
```
```bash
fullPath:c:\jdk1.8\work\PathSeparateTest.java 
path:c:\jdk1.8\work 
fileName:PathSeparateTest.java
```

9-4
```
다음 정의된 메소드를 작성

메서드명 : printGraph
기 능 : 주어진 배열에 담긴 값만큼 주어진 문자를 가로로 출력한 후, 값을 출력한다. 
반환타입 : 없음
매개변수 : int[] dataArr - 출력할 그래프의 데이터
         char ch - 그래프로 출력할 문자.
```

```java
class Exercise9_4 {
static void printGraph(int[] dataArr, char ch) {
      /* 
      (1) printGraph 메소드를 완성하시오.
       */
    for (int i = 0; i < dataArr.length; i ++){
        for(int j = 0; j < dataArr[i]; j++) { // 배열에 저장된 숫자만큼 읽어서 * 출력
            System.out.print(ch); //println하면 다음줄에 입력되니까 가로줄로 출력하려면 그냥 print
        }
        System.out.println(dataArr[i]); // 배열의 수를 출력
    }
}
    public static void main(String[] args) {
        printGraph(new int[]{3, 7, 1, 4}, '*');
    }
}

```

```bash
***3
*******7
*1
****4
```

9-5
```
다음 정의된 메소드를 작성

메서드명 : count
기 능 : 주어진 문자열(src)에 찾으려는 문자열(target)이 몇 번 나오는지 세어서 반환한다. 
반환타입 : int
매개변수 : String src
         String target
[Hint] String클래스의 indexOf(String str, int fromIndex)를 사용할 것
```
```java
class Exercise9_5 {
public static int count(String src, String target) {
    int count = 0; // 찾은 횟수
    int pos = 0; // 찾기 시작할 위치
    
    /* 
      (1) 반복문을 사용해서 아래의 과정을 반복한다. 
      1. src에서 target을 pos의 위치부터 찾는다. 
      2. 찾으면 count의 값을 1 증가 시키고, pos의 값을 target.length만큼 증가시킨다.
      3. indexOf의 결과가 -1이면 반복문을 빠져나가서 count를 반환한다.
    */
    while (true){
        pos = src.indexOf(target,pos); // 1. indexOf()는 지정된 문자열 위치를 반환, 못찾으면 -1 반환
        if (pos != -1) { // 2.
            count++;
            pos += target.length();
        } else {
            break;
        }
    }
    return count; // 3.
    }
    public static void main(String[] args) { 
        System.out.println(count("12345AB12AB345AB","AB"));
        System.out.println(count("12345","AB"));
    }
}
```

```bash
실행결과
3
0
```

9-6
```
다음 정의된 메소드를 작성

메서드명 : fillZero
기 능 : 주어진 문자열(숫자)로 주어진 길이의 문자열로 만들고, 왼쪽 빈 공간은 '0'으로 채운다.
만일 주어진 문자열이 null이거나 문자열의 길이가 length의 값과 같으면 그대로 반환한다.
만일 주어진 length의 값이 0보다 같거나 작은 값이면, 빈 문자열("")을 반환한다.
 
반환타입 : String
매개변수 : String src - 변환할 문자열
         int length - 변환한 문자열의 길이
```
```java
class Exercise9_6 {
    public static String fillZero(String src, int length) {
         /* 
         (1) fillZero메서드를 작성하시오.
          1. src가 널이거나 src.length()가 length와 같으면 src를 그대로 반환한다. 
          2. length의 값이 0보다 같거나 작으면 빈 문자열("")을 반환한다.
          3. src의 길이가 length의 값보다 크면 src를 length만큼 잘라서 반환한다. 
          4. 길이가 length인 char배열을 생성한다.
          5. 4에서 생성한 char배열을 '0'으로 채운다.
          6. src에서 문자배열을 뽑아내서 4에서 생성한 배열에 복사한다.
          7. 4에서 생성한 배열로 String을 생성해서 반환한다.
         */
        if (src == null || src.length() == length) {
            return src;
        } else if (length <= 0) {
            return "";
        } else if (src > length) {
            return src.substring(0, length);
        }
        
        char[] chArr = new char[length];
        
        for(int i=0; i<chArr.length; i++)
            chArr[i] = '0';
        System.arraycopy(src.toCharArray(), 0, chArr, length-src.length(), src.length());
        // 괄호 안은 차례대로 복사하고자 하는 원본소스, 원본 소스에서 어느부분부터 읽어 올 것인지, 
        // 복사하려는 대상 소스, 복사를 어느 부분부터 쓸 것인지, 원본에서 복사본까지 데이터를 얼마만큼 읽어올 것인지를 의미. 
        
        return  new String(chArr);
    }
    
        public static void main(String[] args) { 
        String src = "12345"; 
        System.out.println(fillZero(src,10)); 
        System.out.println(fillZero(src,-1)); 
        System.out.println(fillZero(src,3));
    }
}
```

9-7
```
다음 정의된 메소드를 작성

메서드명 : contains
기 능 : 첫 번째 문자열(src)에 두 번째 문자열(target)이 포함되어 있는지 확인한다. 
       포함되어 있으면 true, 그렇지 않으면 false를 반환한다.
반환타입 : boolean
매개변수 : String src 
         String target
         
[Hint] String클래스의 indexOf()를 사용할 것
```

```java
class Exercise9_7{
    /* 
      (1) contains 메소드를 완성하시오.
     */
    public static boolean contains(String src, String target) {
        return src.indexOf(target) != -1; // src에서 target 위치를 찾아 위치값을 반환. 못찾는 경우 -1을 반환하므로
                                         // 값이 -1인지만 확인해서 리턴하면 된다. 
    }

    public static void main(String[] args) {
        System.out.println(contains("12345", "23"));
        System.out.println(contains("12345", "67"));
    }
}
```

```bash
실행결과
true 
false
```

9-8
```
다음 정의된 메소드를 작성

메서드명 : round
기 능 : 주어진 값을 반올림하여, 소수점 이하 n자리의 값을 반환한다.
예를 들어 n의 값이 3이면, 소수점 4째 자리에서 반올림하여 소수점 이하 3자리의 수를 반환한다.
반환타입 : double
매개변수 : double d - 변환할 값
int n - 반올림한 결과의 소수점 자리

[Hint] Math.round()와 Math.pow()를 이용
```

```java
class Exercise9_8 {
    /* 
      (1) contains 메소드를 완성하시오.
     */
    public static double round(double d, int n) {
        return Math.round(d * Math.pow(10,n)) / Math.pow(10,n); 
        // Math.round는 소수점 첫째 자리 반올림 후 long 타입 정수로 반환
        // Math.pow는 10의 n제곱. 
        // Math.round가 소수점 첫쨰 자리 반올림을 하므로 각 자리수를 맞추기 위해서는 
        // 곱했다가 반올림 계산 후 다시 10의 제곱으로 나눠준다.
    }

    public static void main(String[] args) {
        System.out.println(round(3.1415, 1));
        System.out.println(round(3.1415, 2));
        System.out.println(round(3.1415, 3));
        System.out.println(round(3.1415, 4));
        System.out.println(round(3.1415, 5));
    }
}
```

```bash
실행결과
3.1
3.14
3.142
3.1415
3.1415
```

9-9
```
다음 정의된 메소드를 작성

메서드명 : delChar
기 능 : 주어진 문자열에서 금지된 문자들을 제거하여 반환한다.
반환타입 : String
매개변수 : String src - 변환할 문자열
String delCh - 제거할 문자들로 구성된 문자열

[힌트] StringBuffer와 String클래스의 charAt(int i)과 indexOf(int ch)를 사용.
```

```java
class Exercise9_8 {
    /* 
      (1) delChar 메소드를 완성하시오.
     */
    public static String delChar(String src, String delCh){
        StringBuffer sb = new StringBuffer(src.length()); 
        //문자열 같의 결합, 추출 등을 진행하므로 StringBuffer 클래스가 바람직함
        
        for(int i = 0; i < src.length(); i++){
            char ch = src.charAt(i); // charAt(int i) i번째 문자열을 가져옴
            
            if(delCh.indexOf(ch) == -1) // ch가 delCh에 포함되지 않아 -1을 반환하면,
                sb.append(ch); // sb에 append한다.
        }
        return sb.toString(); // 이를 다시 string으로 리턴
    }

    public static void main(String[] args) {
        System.out.println("(1!2@3^4~5)" + " -> "
                + delChar("(1!2@3^4~5)", "~!@#$%^&*()"));
        System.out.println("(1 2 3 4\t5)" + " -> "
                + delChar("(1 2 3 4\t5)", " \t"));
    }
}
```

```bash
실행결과
(1!2@3^4~5) -> 12345
(1 2 3 4 5) -> (12345)
```

9-10
```
다음 정의된 메소드를 작성

메서드명 : format
기 능 : 주어진 문자열을 지정된 크기의 문자열로 변환한다. 나머지 공간은 공백으로 채운다.
반환타입 : String
매개변수 :  String str - 변환할 문자열
          int length - 변환된 문자열의 길이
          int alignment - 변환된 문자열의 정렬조건 
          (0:왼쪽 정렬, 1: 가운데 정렬, 2:오른쪽 정렬)
```
```java
class Exercise9_10 { 
    /*
    (1) format메서드를 작성하시오.
       1. length의 값이 str의 길이보다 작으면 length만큼만 잘라서 반환한다.
       2. 1의 경우가 아니면, length크기의 char배열을 생성하고 공백으로 채운다. 
       3. 정렬조건(alignment)의 값에 따라 문자열(str)을 복사할 위치를 결정한다.
          (System.arraycopy()사용) 
       4. 2에서 생성한 char배열을 문자열로 만들어서 반환한다.
     */
    public static String format(String str, int length, int alignment){
        int diff = length - str.length();
        if(diff<0)
            return str.substring(0, length); // 1.
        
        char[] source = str.toCharArray(); // 2. 문자열을 배열로 반환
        char[] result = new char[length];
        
        for(int i=0; i <result.lengthl; i++)
            result[i] = ' '; // 공백으로 배열을 채움
        
        switch (alignment){ // alignment 값에 따라 문자열 복사 위치가 결정됨. 
            case 0 : // 왼쪽 정렬
            default:
                System.arraycopy(source, 0, result, 0, source.length);
                break;
            case 1 : // 가운데 정렬
                System.arraycopy(source, 0, result, diff/2, source.length);
            case 2: // 오른쪽 정렬
                System.arraycopy(source, 0, result, diff, source.length);
                break;
        }
        return new String(result); // 2.에서 생성한 배열을 문자열로 만들어서 반환한다. 
    }
    
    
    public static void main(String[] args) { String str = "가나다";
        System.out.println(format(str,7,0)); // 왼쪽 정렬 
        System.out.println(format(str,7,1)); // 가운데 정렬 
        System.out.println(format(str,7,2)); // 오른쪽 정렬
        }
}
```

```bash
가나다 
 가나다 
  가나다
```

9-11
```
커맨드라인으로 2~9사이의 두 개의 숫자를 받아서 두 숫자사이의 구구단을 출력 하는 프로그램을 작성
3, 5를 입력하면 3단부터 5단까지 출력한다.
```

```java
class Exercise9_11 {
    public static void main(String[] args) {
        int from = 0;
        int to = 0;
        
        try {
            if(args.length!=2)
                throw new Exception("시작 단과 끝 단, 두 개의 정수를 입력해주세요.");
            
            from = Integer.parseInt(args[0]);
            to = Integer.parseInt(args[1]);
            
            if(!(2 <= from && from <= 9 && 2 <= to && <=9 ))
                throw new Exception("단의 범위는 2와 9 사이의 값이어야 합니다.");
        } catch(Exception e) {
            System.out.println(e.getMessage());
            System.out.println("USAGE: GugudanTest 3 5");
            System.exit(0);
        }
        
        if (from > to) {
            int tmp = from;
            from = to;
            to = tmp;
        }
        
        for (int i = from; i<to; i++) {
            for (int j = 1; j <= 9; j++) {
                System.out.println(i + "*" + j + "=" + i * j);
            }
            System.out.println();
        }  
    } // main
}
```

```bash
실행 결과

C:\jdk1.8\work\ch9>java Exercise9_11 2 시작 단과 끝 단, 두 개의 정수를 입력해주세요. 
USAGE : GugudanTest 3 5

C:\jdk1.8\work\ch9>java Exercise9_11 1 5 단의 범위는 2와 9사이의 값이어야 합니다.
USAGE : GugudanTest 3 5

C:\jdk1.8\work\ch9>java Exercise9_11 3 5 3*1=3
3*2=6
3*3=9
3*4=12
3*5=15
3*6=18
3*7=21
3*8=24
3*9=27

4*1=4
4*2=8
4*3=12
4*4=16
4*5=20
4*6=24
4*7=28
4*8=32
4*9=36

5*1=5
5*2=10
5*3=15
5*4=20
5*5=25
5*6=30
5*7=35
5*8=40
5*9=45
```


9-12
```
다음 정의된 메소드를 작성

메서드명 : getRand
기 능 : 주어진 범위(from~to)에 속한 임의의 정수값을 반환한다.
        (양쪽 경계값 모두 범위에 포함)
        from의 값이 to의 값보다 클 경우도 처리되어야 한다.
반환타입 : int
매개변수 : int from - 범위의 시작값
         int to - 범위의 끝값

[힌트] Math.random()과 절대값을 반환하는 Math.abs(int a), 
그리고 둘 중에 작은 값을 반환하는 Math.min(int a, int b)를 사용하라.
```

```java
class Exercise9_12{
     /* 
      (1) getRand 메소드를 완성하시오.
     */
    public static int getRand(int from, int to) {
        return (int) (Math.random() * (Math.abs(to-from)+1)) + Math.min(from,to);
        // to-from = 끝값-시작값, abs는 from 값이 to보다 클 경우를 대비해 절대값 처리. 
    }
    
     public static void main(String[] args){
         for(int i=0; i< 20; i++) 
             System.out.print(getRand(1,-3)+",");
     }
}
```

```bash
실행결과
0,-1,1,0,-2,-2,1,1,-3,0,-1,1,1,1,0,-1,1,0,-1,-3,
```

9-13
```
하나의 긴 문자열(source) 중에서 특정 문자열과 일치하는 문자열의 개수 를 구하는 예제
빈 곳 채워 완성
```
```java
public class Exercise9_13 {
    public static void main(String[] args) {
        String src = "aabbccAABBCCaa";
        System.out.println(src);
        System.out.println("aa를 " + stringCount(src, "aa") +"개 찾았습니다.");
    }
    
    static int stringCount(String src, String key) {
        return stringCount(src, key, 0);
    }

    static int stringCount(String src, String key, int pos) { 
        int count = 0;
        int index = 0;

        if (key == null || key.length() == 0) 
            return 0;

        /* (1) 알맞은 코드를 넣어 완성하시오. */
        while((index = src.indexOf(key, pos))!= -1){ // 해당 문자열이 존재하지 않을 때(반환값이 -1 일때)까지 반복
            count++; // 일치하는 부분을 찾으면 count 1 증가
            pos = index + key.length(); // 검색 시작 위치 변경
        }
        return count;
    }
}
```

```bash
실행결과
aabbccAABBCCaa 
aa를 2개 찾았습니다.
```


9-14
```
화면에서 전화번호 일부를 입력받아 일치하는 전화번호를 주어진
문자열 배열에서 찾고 출력하는 프로그램을 완성

[Hint] Pattern, Matcher클래스를 사용할 것
```

```java
import java.util.*; 
import java.util.regex.*;

class Exercise9_14 {
    public static void main(String[] args) {
        String[] phoneNumArr = {
                "012-3456-7890",
                "099-2456-7980",
                "088-2346-9870",
                "013-3456-7890"
        };

        ArrayList list = new ArrayList();
        Scanner s = new Scanner(System.in);
        while (true) {
            System.out.print(">>");
            String input = s.nextLine().trim();

            if (input.equals("")) {
                continue;
            } else if (input.equalsIgnoreCase("Q")) {
                System.exit(0);
            }
            
            /* (1) 알맞은 코드를 넣어 완성하시오. */
            String pattern = ".*"+input+".*"; // input 포함 모든 문자열
            Pattern p = Pattern.compile(pattern);
            
            for(int i=0; i<phoneNumArr.length; i++){
                String phoneNum = phoneNumArr[i];
                String tmp = phoneNum.replace("-", ""); //전화번호에서 - 제거
                
                Matcher m = p.matcher(tmp);
                
                if(m.find()){ // 패턴과 일치하면 리스트에 추가
                    list.add(phoneNum);
                }
            }
            
            
            if (list.size() > 0) {
                System.out.println(list);
                list.clear();
            } else {
                System.out.println("일치하는 번호가 없습니다.");
            }
        }
    } //main
}

```


```bash
실행결과
>>
>>asdf
일치하는 번호가 없습니다.
>>
>>
>>0
[012-3456-7890, 099-2456-7980, 088-2346-9870, 013-3456-7890] 
>>234
[012-3456-7890, 088-2346-9870]
>>7890
[012-3456-7890, 013-3456-7890]
>>q
```
