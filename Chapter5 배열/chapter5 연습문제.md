5-1     
잘못된 것?

```java
a. int[] arr[];
b. int[] arr = {1,2,3,};
c. int[] arr = new int[5];
d. int[] arr = new int[5]{1,2,3,4,5};
e. int arr[5]; 
f. int[] arr[] = new int[3][];
```
d: {} 안에 들어가는 elements에 따라 배열 크기가 지정되는데, 여기서는 []안에 크기를 미리 지정했으므로 잘못 되었다.
e: 배열의 선언부에는 크기를 지정할 수 없다. new 로 생성과 동시에 크기 지정.

5-2     
arr[3].length의 값?
```java
int[][] arr = {
    { 5,5,5,5,5},
    { 10, 10, 10},
    { 20, 20, 20, 20}, 
    { 30, 30}
}
```
3번째 arr은 { 30, 30} 이므로, length는 2가 된다.


5-3     
arr에 담긴 모든 값을 더하는 프로그램 완성

```java
class Exercise5_3{
    public static void main(Strign[] args){
        int[] arr = {10,20,30,40,50};
        int sum = 0;

        for (int i = 0; i < arr.legnth; i++){
            sum += arr[i];
        }
        System.out.println("sum="+sum);
    }
}
```
5-4     
2차원 배열 arr에 담긴 모든 값의 총합과 평균을 구하는 프로그램 완성

```java
class Exercise5_4 {
    public static void main(Strign[] args) {
        int[][] arr = {
                { 5, 5, 5, 5, 5},
                {10,10,10,10,10},
                {20,20,20,20,20},
                {30,30,30,30,30}
        };
        int total = 0;
        float average = 0;
        
        for(int i = 0; i < arr.length; i++) {
            for(int j = 0; j < arr[i].length; j++) {
                total += arr[i][j];
            }
        }
        average = total / (float)(arr.length * arr[0].length); // 소수점 이하 자리수까지 얻기 위해 float 형변환
        System.out.println("total="+total);
        System.out.println("average="+average);
    } //end of main
} //end of class
```

5-5     
1~9 사이의 중복되지 않은 숫자로 이루어진 3자리 숫자를 만드는 프로그램 완성.

```java
class Exercise5_5 {
    public static void main(Strign[] args) {
        int[] ballArr = {1,2,3,4,5,6,7,8,9}; 
        int[] ball3 = new int[3];

        // 배열 ballArr의 임의의 요소를 골라서 위치를 바꾼다. 
        for(int i=0; i< ballArr.length; i++) {
            int j = (int) (Math.random() * ballArr.length);
            int tmp = 0;
            
            tmp = ballArr[i]; // ballArr[i], ballArr[j] 자리 변경
            ballArr[i] = ballArr[j];
            ballArr[j] = tmp;
        }
        // 배열 ballArr의 앞에서 3개의 수를 배열 ball3로 복사한다.
        System.arraycopy(ballArr, 0, ball3, 0, 3); //byte[] 형태의 데이터를 자르거나 연접하기 위해 사용
        // 괄호 안은 차례대로 복사하고자 하는 원본소스, 원본 소스에서 어느부분부터 읽어 올 것인지, 
        // 복사하려는 대상 소스, 복사를 어느 부분부터 쓸 것인지, 원본에서 복사본까지 데이터를 얼마만큼 읽어올 것인지를 의미. 
        for(int i=0;i<ball3.length;i++) { 
            System.out.print(ball3[i]);
        }
        System.out.println(); 
    } // end of main
} // end of class
```

5-6     
거스름돈을 몇 개의 동전으로 할 수 있는지 계산하는 문제.        
변수  money의 금액을 동전으로 바꿨을 때 각각 동전이 몇 개 필요한지 계산해서 출력.
나눗셈 연산자와 나머지 연산자를 사용할 것!
```java
class Exercise5_6 {
    public static void main(Strign[] args) {
        // 큰 금액의 동전을 우선적으로 거슬러 줘야 한다.
        int[] coinUnit = {500, 100, 50, 10};
        
        int money = 2680;
        System.out.println("money="+money);
        
        for(int i = 0; i<coinUnit.length; i++){
            System.out.println(coinUnit[i]+"원: "+money/coinUnit[i]); // 동전 큰 단위부터 나눠서 거스름돈 객수를 줄임
            money = money%coinUnit[i]; // 나머지 연산으로 거스름돈 지불 후 남은 금액 계산. 이후 계속 반복. 
        }
    } // main
}
```
5-7     

```java
class Exercise5_7 {
    public static void main(Strign[] args) {
        if(args.length!=1) {
            System.out.println("USAGE: java Exercise5_7 3120");
            System.exit(0);
        }

        // 문자열을 숫자로 변환한다. 입력한 값이 숫자가 아닐 경우 예외가 발생한다. 
        int money = Integer.parseInt(args[0]);

        System.out.println("money="+money);
        
        int[] coinUnit = {500, 100, 50, 10}; //동전의 단위
        int[] coin     = {5, 5, 5, 5}; //단위별 동전의 개수

        for(int i=0;i<coinUnit.length;i++) {
            int coinNum = 0;
            // 1. 금액(money)을 동전단위로 나눠서 필요한 동전의 개수(coinNum)를 구한다.
            coinNum = money / coinUnit[i];
            // 2. 배열 coin에서 coinNum만큼의 동전을 뺀다.
            // (만일 충분한 동전이 없다면 배열 coin에 있는 만큼만 뺀다.) 
            if(coin[i] >= coinNum) {
                 coin[i] -= coinNum; 
            } else {
                coinNum = coin[i]; 
                coin[i] = 0;
            }
            // 3. 금액에서 동전의 개수(coinNum)와 동전단위를 곱한 값을 뺀다.
            money -= coinNum * coinUnit[i];

            System.out.println(coinUnit[i]+"원: "+ coinNum);
        }
        if(money > 0) {
            System.out.println("거스름돈이 부족합니다.");
            System.exit(0); // 프로그램을 종료한다.
        }

        System.out.println("=남은 동전의 개수 =");
        
        for(int i=0; i<coinUnit.length;i++){
            System.out.println(coinUnit[i]+"원:"+coin[i]);
        }
    } // main
}
```
5-8     
배열 answer에 담긴 데이터를 읽고 각 숫자의 개수를 세어서 개수만큼 *을 찍는 프로그램.

```java
class Exercise5_8 {
    public static void main(Strign[] args) {
        int[] answer = { 1,4,4,3,1,4,4,2,1,3,2 }; 
        int[] counter = new int[4]; // 숫자 범위가 1~4까지이므로 크기가 4인 배열 생성

        for(int i=0; i < answer.length; i++) {
            counter[answer[i]-1]++; // -1은 index 범위가 0~3이어서 해주는 것. 
        }

        for(int i=0; i < counter.length;i++) {
            System.out.print(counter[i]);

            for (int j = 0; j < counter[i]; j++) {
                System.out.print("*"); 
            }
            System.out.println();
        }
    } // end of main
} // end of class
```

5-9     
주어진 배열을 시계방향 90도 회전시키는 프로그램

```java
class Exercise5_9 {
    public static void main(Strign[] args) {
        char[][] star = {
                {'*', '*', ' ', ' ', ' '},
                {'*', '*', ' ', ' ', ' '},
                {'*', '*', '*', '*', '*'},
                {'*', '*', '*', '*', '*'}
        };

        char[][] result = new char[star[0].length][star.length];

        for (int i = 0; i < star.length; i++) {
            for (int j = 0; j < star[i].length; j++) {
                System.out.print(star[i][j]);
            }
            System.out.println();
        }

        System.out.println();

        for (int i = 0; i < star.length; i++) {
            for (int j = 0; j < star[i].length; j++) {
                // 알맞은 코드를 넣어 완성
                int x = j; // 90도 회전시 4*5 배열이 5*4 배열로 바뀌고, x 값은 j 값과 일치한다. 
                int y = star.length-1-i; // i+y=star.length-1 -> 'y=star.length-1-i'
                
                result[x][y]=star[i][j];
            }
        }
        for (int i = 0; i < result.length; i++) {
            for (int j = 0; j < result[i].length; j++) {
                System.out.print(result[i][j]);
            }
            System.out.println();
        }
    } // end of main
} // end of class
```

5-10        
알파벳과 숫자를 암호표로 암호화 하는 프로그램 완성

```java
```

```java
```
```java
```

```java
```


