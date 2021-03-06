>πμΈνλ° - **`μλ¦¬ν νλ‘κ·Έλλ°μ μν μκ³ λ¦¬μ¦ κ°μ’`** λ₯Ό κ³΅λΆνλ©° μ λ¦¬ν λ΄μ©

<br>

# 1-3. Recursionμ κ°λκ³Ό κΈ°λ³Έ μμ 
#### Designing Recursion <i>μν μκ³ λ¦¬μ¦μ μ€κ³</i>
<br>

### μμ½
```
[μνμ  μκ³ λ¦¬μ¦ μ€κ³]
β  μ μ΄λ νλμ base case, μ¦ μνλμ§ μκ³  μ’λ£λλ caseκ° μμ΄μΌ ν¨.
β‘ λͺ¨λ  caseλ κ²°κ΅­ base caseλ‘ μλ ΄ν΄μΌ ν¨.
``` 
<br>

μμμ (implicit) λ§€κ°λ³μλ₯Ό **`λͺμμ (explicit) λ§€κ°λ³μ`**λ‘ λ°κΎΈμ΄λΌ.
<br>
<br>

## 1. μμ°¨ νμ
```java
int search(int[] data, int n, int target) {
    for (int i = 0; i < n; i++) {
        if (data[i] == target) {
            return i;
        }
    }
    return -1;
}
```
- μ΄ ν¨μμ λ―Έμμ data[0]μμ data[n-1] μ¬μ΄μμ targetμ κ²μνλ κ²μ΄λ€.  
νμ§λ§ κ²μ κ΅¬κ°μ μμ μΈλ±μ€ 0μ λ³΄ν΅ μλ΅νλ€. μ¦ <u>**`μμμ  λ§€κ°λ³μ`**</u>μ΄λ€.
  - n-1μ λͺμμ μΌλ‘ ννν΄λ¨μ§λ§, 0μ μμλ κ².  
    (0λΆν° μμν  κ²μ΄λΌκ³  μλ¬΅μ μΌλ‘ λμ)


- μμμ κ΄λ ¨ν΄μ νΉμ  μ‘°κ±΄μ΄ μ£Όμ΄μ§μ§ μλλ€λ©΄, μ μΌν λ°©λ²μ νλμ© μμλλ‘ λ³΄λ κ²μ΄λ€.
  - μμκ° μ λ ¬λμ΄ μλ€λ©΄? μ΄μ§ κ²μ μ¬μ©.
- μμ°¨μ μΌλ‘ κ²μ¬ν΄μ νκ²μ μ°Ύκ³ , λκΉμ§ κ²μ¬νμΌλ νκ²μ΄ μλ€λ©΄ return -1;
<br>
<br>

## 2. λ§€κ°λ³μμ λͺμν: μμ°¨ νμ
```java
int search(int[] data, int begin, int end, int target) {

    if (begin > end) {
        return -1;
    } else if (target == data[begin]) {
        return begin;
    } else {
        return search(data, begin+1, end, target);
    }
}
```
- μ΄ ν¨μμ λ―Έμμ data[begin]μμ data[end] μ¬μ΄μμ targetμ κ²μνλ€. μ¦, κ²μκ΅¬κ°μ μμμ μ λͺμμ (explicit)μΌλ‘ μ§μ νλ€.
- μ΄ ν¨μλ₯Ό search(data, 0, n-1, target)μΌλ‘ νΈμΆνλ€λ©΄ μ νμ΄μ§μ ν¨μμ μμ ν λμΌν μΌμ νλ€.
<br>
<br>

### 2.1 μμ°¨ νμ: λ€λ₯Έ λ²μ  (1)
```java
int searchReverse(int[] data, int begin, int end, int target) {

    if (begin > end) {
        return -1;
    } else if (target == data[end]) {
        return end;
    } else {
        return search(data, begin, end-1, target);
    }
}
```
- λ΄κ° μ°Ύλ κ°κ³Ό λ§μ§λ§ κ°μ λΉκ΅ν΄μ μ°Ύλλ€. (λ€μμλΆν° λΉκ΅)
<br>
<br>

### 2.2 μμ°¨ νμ: λ€λ₯Έ λ²μ  (2)
```java
// ? debugging νμ.
static int searchUsingMid(int[] data, int begin, int end, int target) {

    if (begin > end) {
        return -1;
    } else {
        int middle = (begin+end)/2;
        if (data[middle] == target) {
            return middle;
        }
        int index = searchUsingMid(data, begin, middle - 1, target);
        if (index != -1) {
            return index;
        } else {
            return searchUsingMid(data, middle + 1, end, target);
        }
    }//else
}
```
- binary searchμλ λ€λ₯΄λ€.
- beginκ³Ό endλ‘ κ²μμ§μ μ μ€μ νκ³ , middleμ μ€μ ν ν μμͺ½μμ κ²μ¬ν΄λ³΄κ³  μμͺ½μμ targetμ λ°κ²¬νμ§ λͺ»νλ€λ©΄ middle λ·μͺ½μ κ²μ¬νλ€. 
- // ? int index κ° κ°λ¦¬ν€λ μ§μ , return -1 λλ μ§μ μ΄ μμ²­ ν·κ°λ¦°λ€.
<br>
<br>


## 3. λ§€κ°λ³μμ λͺμν: μ΅λκ° μ°ΎκΈ°
```java
int findMax(int[] data, int begin, int end) {
    if (begin == end) {
        return data[begin];
    } else {
        return Math.max(data[begin], findMax(data, begin + 1, end));
    }
}
```
- μ΄ ν¨μμ λ―Έμμ data[begin]μμ data[end] μ¬μ΄μ μ΅λκ°μ μ°Ύμ λ°ννλ€.  
(begin <= endλΌκ³  κ°μ νλ€.)

- int[] data = {8, 5, 17, 9, 58};
- findMax(1,4)
  - return max(data[1], **`findMax(2,4)`**)
      - return max(data[2], **`findMax(3,4)`**)
        - return max(data[3], **`findMax(4,4)`**)
          - return data[4]
        - return max(data[3], **data[4]**) -> data[4]
      - return max(data[2], **data[4]**) -> data[4]
  - return max(data[1], **data[4]**) -> data[4]
- κ²°κ³Ό: data[4]
- λ°μ΄ν° κ²μ κ΅¬κ°μ΄ μκΎΈ λ³νλ κ²½μ° λͺμμ μΌλ‘ νννλ κ²μ΄ μ’λ€.
<br>
<br>


### 3.1 μ΅λκ° μ°ΎκΈ°: λ€λ₯Έ λ²μ 
```java
static int findMaxUsingMid(int[] data, int begin, int end) {
    if (begin == end) {
        return data[begin];
    } else {
        int middle = (begin+end)/2;
        int max1 = findMaxUsingMid(data, begin, middle);
        int max2 = findMaxUsingMid(data, middle + 1, end);
        return Math.max(max1, max2);
    }
}
```
- beginμμ endκΉμ§ μ€μμ middleμ κΈ°μ€μΌλ‘ μμͺ½μμ μ΅λκ° νλ(max1), λ·μͺ½μμ μ΅λκ° νλ(max2)λ₯Ό μ°Ύμ ν max1κ³Ό max2λ₯Ό λΉκ΅νλ€. 
- // ? max1 μ κ΅¬νλλ°, max2 λΆλΆ λ§€κ°λ³μλ₯Ό μ΄λ€ κ±Έ λ€κ³  λ€μ΄κ°μΌνλμ§, return νμ λ μ΄λλ‘ λμκ°μΌ νλμ§ λλ²κΉν΄λ λͺ¨λ₯΄κ² μ΄μ λμ΄κ°λ€.
<br>
<br>



## 4. Binary Search
```java
public static int binarySearch(String[] items, String target, int begin, int end) {
    if (begin > end) {
        return -1;
    } else {
        int middle = (begin + end) /2;
        int compResult = target.compareTo(items[middle]);
        if (compResult == 0) {
            return middle;
        } else if (compResult < 0) {
            return binarySearch(items, target, begin, middle - 1);
        } else {
            return binarySearch(items, target, middle + 1, end);
        }
    }
}
```
