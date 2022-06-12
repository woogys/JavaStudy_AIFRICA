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
```java
class Exercise5_6 {
    public static void main(Strign[] args) {
        // 큰 금액의 동전을 우선적으로 거슬러 줘야 한다.
        int[] coinUnit = {500, 100, 50, 10};
        
        int money = 2680;
        System.out.println("money="+money);
        
        for(int i = 0; i<coinUnit.length; i++){
            System.out.println(coinUnit[i]+"원: "+money/coinUnit[i]);
            money = money&coinUnit[i];
        }
    } // main
}
```

```java
```

```java
```

```java
```
