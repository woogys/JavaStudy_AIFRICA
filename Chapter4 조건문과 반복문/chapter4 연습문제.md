4-1 

1. 10 < x && x < 20
2. !(ch ==' ' || ch == '\t')
3. ch == 'x' || ch == 'X'
4. '0' <= ch && ch <= '9'
5. ('a'<=ch&&ch<='z') || ('A'<=ch&&ch<='Z')
6. year%400==0 || year%4==0 && !(year%100=0)
7. !powerOn
8. str.equals("yes")

4-2

class 4_2 {
    public static void main(String[] args) {
        int sum = 0;

        for (int i=1; i <=20; i++) {
            if (i%2!=0 && i%3!=0)
                sum += i;
        }
        System.out.println(sum);
    }
}

4-3

class 4_3 {
    public static void main(String[] args) {
        int sum = 0;
        int total = 0;    

        for (int i=1; i<=10; i++){
            sum += i;
            total += sum;
        }
        System.out.println(total);
    }
}

4-4

class 4_4{
    public static void main(String[] args) {
        int sum = 0;
        int s = 1;
        int num = 0;

        for (int i = 1; true; i++, s=-s){ // 조건문이 true거나 비어있으면 무한반복
            num = s * i;
            sum += num;

            if(sum>=100)
                break;
        }
        System.out.println("num");
        System.out.println("sum");
    }
}

4-5

class 4_5 {
    public static void main(String[] args) {
        int i = 0;
        while(i<=10) {
            int j = 0;
            while(j<=i) {
                System.out.print("*");
                j++;
            }
            System.out.println();
            i++;
        }
    }
}

4-6

class 4_6 {
    public static void main(String[] args) {
        for(int i=1; i<=6; i++)
            for(int j=i; j<=6; j++)
                if (i+j==6)
                    System.out.println(i+"+"+j+"="+(i+j));
    }
}

4-7

class 4_7 {
    public static void main(String[] args) {
        int value = (int)(Math.random()*6)+1;

        System.out.println("value:"+value); 
    }
}

4-8

class 4_8 {
    public static void main(String[] args) {
        for (int x = 0; x<=10; i++){
            for(int y = 0; y<=10; j++){
                if(2*x+4*y==10){
                    System.out.println("x=" + x + ", y=" + y);
                }
            }
        }
    }
}

4-9

class 4_9 {
     public static void main(String[] args) {
         String str = "12345";
         int sum = 0;

         for (int i = 0; i < str.length(); i++) {
             sum += str.charAt(i) - '0';
         }

         System.out.println(sum);
    }
}

4-10

class 4_10 {
     public static void main(String[] args) {
         int num = "12345";
         int sum = 0;

         while(num>0){
             sum += num%10;
             num /= 10;
         }

         System.out.println(sum);
    }
}

4-11

class 4_11 {
    public static void main(String[] args) {
        int num1 = 1;
        int num2 = 2;
        int num3 = 0;
        System.out.print(num1+","+num2);

        for (int i = 0; i < 8; i++){
            num3 = num1 + num2;
            System.out.println(","+num3);

            num1 = num2;
            num2 = num3;
        }
    }
}

4-12

class 4_12 {
    public static void main(String[] args) {
        for (int i = 1; i<=9; i++){
            for (int j = 1; j<= 3; j++) {
                int x = j+1+(i-1)/3*3;
                int y = i%3==0?
            }
        }
    }
}

4-13

class 4_13 {
    public static void main(String[] args) {
        String value = "12o34";
        char ch = ' ';
        boolean isNumber = true; 

        for (int i =0; i < value.length(); i++){
              ch = value.charAt(i);
               if (!('0'<= ch && <= '9')){
                isNumber = false;
                break;
            }
        }

        if (isNumber){
            System.out.println(value+"는 숫자입니다.");
        } else {
            System.out.pirntln(value+"는 숫자가 아닙니다.");
        }
    }
}

4-14

(1) (int)(Math.random()*100)+1;
(2) 
    if(input<answer) {
        System.out.println("더 큰 수를 입력하세요.");
    } else if(answer<input){
        System.out.println("더 작은 수를 입력하세요.");
    } else {
        System.out.println("맞췄습니다");
        System.out.println("시도 횟수는 "+count+"번입니다.");
        break;
    }

4-15

result = result*10 + tmp%10;
tmp /= 10;