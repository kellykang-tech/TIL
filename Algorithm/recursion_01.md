>๐์ธํ๋ฐ - **`์๋ฆฌํ ํ๋ก๊ทธ๋๋ฐ์ ์ํ ์๊ณ ๋ฆฌ์ฆ ๊ฐ์ข`** ๋ฅผ ๊ณต๋ถํ๋ฉฐ ์ ๋ฆฌํ ๋ด์ฉ

<br>

# 1-1. Recursion์ ๊ฐ๋๊ณผ ๊ธฐ๋ณธ ์์ 

## Recursion (์ํ)
- ์๊ธฐ ์์ ์ ํธ์ถํ๋ ํจ์
- ์ํ ํน์ ์ฌ๊ทํจ์๋ผ๊ณ  ๋ถ๋ฅธ๋ค.

```java
public class Code01 {
    
    public static void main(String[] args){
        func();
    }


    public static void func(){
        System.out.println("Hello");
        func();
    }
}
```

- run: ๋ฌดํ๋ฃจํ์ ๋น ์ง
```java
Hello
Hello
Hello
Hello
...
```
<br>

## 1. recursion์ ํญ์ ๋ฌดํ๋ฃจํ์ ๋น ์ง๊น?
```java
public class Code02 {

    public static void main(String[] args) {
        int n = 4;
        func(n);
    }

    public static void func(int k) {
        if (k <= 0) {
            return;
        } else {
            System.out.println("Hello");
            func(k - 1);
        }
    }
```
- ์ฝ๋๋ฅผ ์ด๋ป๊ฒ ์์ฑํ๋๋์ ๋ฐ๋ผ ๋ฌดํ๋ฃจํ์ ๋น ์ง ์๋ ๋น ์ง์ง ์์ ์๋ ์๋ค. 
- k๊ฐ 0๋ณด๋ค ์๊ฑฐ๋ ๊ฐ์ผ๋ฉด **`return`**.
  - return ํ๊ฒ ๋๋ฉด ์ปจํธ๋กค์ ํญ์ ์๊ธฐ ์์ ์ ํธ์ถํ๋ ๋ฌธ์ฅ์ผ๋ก ๋์ด๊ฐ๋ค.  
  - else ๋ฌธ ์์ func(0);์ผ๋ก ๋์ด๊ฐ๊ณ  ์ข๋ฃ-> func(1); ์ข๋ฃ -> func(2); ์ข๋ฃ-> func(3); ์ข๋ฃ -> func(4); ์ข๋ฃ ๋ฉ์ธ ๋ฉ์๋ func(4); }๋ฅผ ๋น ์ ธ๋์ค๋ฉฐ ๋ฉ์๋ ์ข๋ฃ. 
- run
```
Hello
Hello
Hello
Hello
```
<br>
<br>

## 2. ๋ฌดํ๋ฃจํ์ ๋น ์ง์ง ์์ผ๋ ค๋ฉด?
```java
public static void func(int k) {
        if (k <= 0) {
            return;
        } else {
            System.out.println("Hello");
            func(k - 1);
        }
    }
```

### 2.1 Base case
```java
if (k <= 0)
    return;
```
์ ์ด๋ ํ๋์ recursion์ ๋น ์ง์ง ์๋ ๊ฒฝ์ฐ๊ฐ ์กด์ฌํด์ผ ํ๋ค.
<br>


### 2.2 Recursive case
```java
else 
    System.out.println("Hello");
    func(k - 1);    
```
- recursion์ ๋ฐ๋ณตํ๋ค๋ณด๋ฉด ๊ฒฐ๊ตญ base case๋ก ์๋ ดํด์ผ ํ๋ค.
- ๋จ์ํ base case๊ฐ ์กด์ฌํ๋ค๋ ๊ฒ๋ง์ผ๋ก ๋ฌดํ๋ฃจํ์ ๋น ์ง์ง ์๋ ๊ฒ์ ์๋๋ค.  
base case๊ฐ ์์ด๋ `func(k + 1)`์ธ ๊ฒฝ์ฐ์๋ ๋ค์ ๋ฌดํ๋ฃจํ์ ๋น ์ง๊ฒ ๋๋ค.
<br>
<br>


## 3. 1 ~ n๊น์ง์ ํฉ
```java
public class Code03 {

    public static void main(String[] args) {
        int result = func(4);
        System.out.println("result = " + result);
    }

    public static int func(int n) {
        if (n == 0) {
            return 0;
        } else {
            return n + func(n - 1);
        }
    }
}
```
- run:  
 `result = 10`
- func(4):  
  return 4 + func(3);
    - func(3):  
  return 3 + func(2);
        - func(2):  
  return 2 + func(1);
            - func(1):  
  return 1 + func(0);  
                - func(0):  
                    return 0;


### 3.1 recursion์ ํด์
```java
public static int func(int n) {     //1
        if (n == 0) {
            return 0;               //2
        } else {
            return n + func(n - 1); //3
        }
}
```
- 1๋ฒ: ์ด ํจ์์ mission์ 0 ~ n๊น์ง์ ํฉ์ ๊ตฌํ๋ ๊ฒ์ด๋ค.
- 2๋ฒ: n = 0์ด๋ผ๋ฉด ํฉ์ 0์ด๋ค.
- 3๋ฒ: n์ด 0๋ณด๋ค ํฌ๋ค๋ฉด 0์์ n๊น์ง์ ํฉ์ 0์์ n-1๊น์ง์ ํฉ์ n์ ๋ํ ๊ฒ์ด๋ค.
<br>
<br>


## 4. Factorial: n!
```
0! = 1
n! = n x (n-1)!     * n > 0
```
0!์ 0์ด ์๋๊ณ  1์ด๋ค. (Factorial์ ์ ์)

```java
public static int factorial(int n) {
    if (n == 0) {
        return 1;
    } else {
        return n * factorial(n - 1);
    }
}
```
<br>
<br>


## 5. X<sup>n</sup>

> if n > 0  
    X<sup>0</sup> = 1  
    X<sup>n</sup> = X * X<sup>n-1</sup>   

```java
public static double power(double x, int n) {
    if (n == 0) {
        return 1;
    } else {
        return x * power(x, n - 1);
    }
}
```
<br>
<br>


## 6. Fibonacci Number
>์กฐ๊ฑด: n > 1  
    f<sub>0</sub> = 0  
    f<sub>1</sub> = 1  
    f<sub>n</sub> = f<sub>n-1</sub> + f<sub>n-2</sub>
- 0๋ฒ์งธ ํผ๋ณด๋์น ์ = 0  
- 1๋ฒ์งธ ํผ๋ณด๋์น ์ = 1
- n๋ฒ์งธ ํผ๋ณด๋์น ์   
    = n-1๋ฒ์งธ ํผ๋ณด๋์น ์ + n-2๋ฒ์งธ ํผ๋ณด๋์น ์


```java
public int fibonacci(int n) {
    if (n < 2) {
        return n;
    } else {
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```
<br>
<br>


## 7. ์ต๋ ๊ณต์ฝ์: Euclid Method

### 7.1 Euclid Method 
```java
public static double gcd(int m, int n) {
    if (m < n) {
        int tmp = m;
        m = n;
        n = tmp;    //swap m and n
    }
    
    // 12, 8
    if (m % n == 0) {
        return n;
    } else {
        return gcd(n, m%n);   //8, 4
    }
}
```
m >= ์ธ ๋ ์์ ์ ์ m๊ณผ n์ ๋ํด์ m์ด n์ ๋ฐฐ์์ด๋ฉด gcd(m, n) = n์ด๊ณ , ๊ทธ๋ ์ง ์์ผ๋ฉด gcd(m, n) = gcd(n, m%n)์ด๋ค.
<br>


### 7.2 Euclid Method: ์ข ๋ ๋จ์ํ ๋ฒ์ 

```java
public static int gcdSimple(int p, int q) {
    // 12, 8
    if (q == 0) {
        return p;
    } else {
        return gcdSimple(q, p%q);   //8, 4
    }
}
```
<br>
<br>

     