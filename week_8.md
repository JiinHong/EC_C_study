# 8주차

내용: 기말 내용 총정리 및 예제

<br/>

### 1. 총정리 예제

<br/>

예제 1

```c
#include <stdio.h>

int main()
{
    int x= -5;
    printf("%d\n", x++);
    printf("%d\n", ++x);
    printf("%d\n", -10<x && x<0);
}
```  


<br/>

예제 2

```c
#include <stdio.h>
void prin(int n);
void main() { prin(7); }
void prin(int n)
{
	if (n > 4)
	{
		printf("%d\n", n);
		prin(n - 1);
	}
	printf("%d\n", n);
}
```  

<br/>

예제 3

```c
#include <stdio.h>
void main()
{
	int data[8] = {1, 2, 3, 4, 5, 7, 8};
	int *ptr, i;
	ptr = data;
	*ptr = 500;
	*ptr++ = 300;
	*++ptr = 400;
	for (i = -2; i < 4; i++)
		printf("%4d\n", *(ptr + i));
}
```  

<br/>


예제 4  

다음 자료 형태를 구조체로 선언해보세요.  
구조체 이름은 "SCORE"로 작성하세요!

|std_no|name|kor|eng|mat|
|--------|--------|---|---|---|
|char[10]|char[10]|int|int|int|

<br/>

예제 5

```c
#include <stdio.h>
void func1(int a) { a += 20; }
void func2(int *a) { *a += 20; }
void main()
{
	int num = 10;
	func1(num);
	printf("func1 = %d\n", num);
	func2(&num);
	printf("func2 = %d\n", num);
}
```

<br/>

예제 6  

배열 arr에 있는 값 중에서 최대값을 구하는 max 함수와 최솟값을 구하는 min 함수를 작성해보세요!
  
```c
#include <stdio.h>
void main()
{
	int arr[9] = {20, 50, 40, 90, 100, 10, 30, 80, 70};
	printf("최대값 : %d \n", max(arr));
	printf("최소값 : %d \n", min(arr));
}
```  

<br/>

예제 7  


```c
#include <stdio.h>
void main()
{
	int data[3] = {10, 20, 30};
	int *ptr = data;
	printf("%u \n", ++*ptr);
	printf("%u \n", (*ptr)++);
}
```

<br/>

예제 8  

```c
#include <stdio.h>
#include <string.h>

void main() {
    char str1[20] = "Hello_";
    char str2[20] = "Everyone";
    char *result;

    printf("결과 = %d\n", strcmp(str1, str2)); // 아스키코드 차이를 출력

    result = strcat(str1, str2); // 두 문자열을 이어붙임
    printf("결과 = %s\n", result);

    result = strchr(str1, 'E'); // 해당 문자의 주소를 반환
    *result = '\0';
    printf("결과 = %s\n", str1);

    /*
    이 외에도 strlen, strcpy 한 번씩 확인
    */
}
```


<br/>

예제 9  
포인터와 swap 함수를 이용하여 a = 100과 b = 200의 값을 바꾸어 출력하는 프로그램을 작성해보세요!

예시 결과
```
swap 전
a = 100, b = 200

swap 후
a = 200, b = 100
```

<br/>

예제 10  
Recursion(재귀함수)를 이용하여 팩토리얼 함수(int factorial(int n))를 작성하세요.

예시 결과
```
n을 입력하세요 : 5
5! = 120
```


<br/>

예제 11

```c
#include <stdio.h>

int main()
{
	char arr[] = "korea";
	char *p = arr;
	char ch1 = *p;
	char ch2 = *(p++);
	char ch3 = *(++p);
	char ch5 = *p;
	char ch4 = ++*p;

	printf("%c, %c, %c, %c, %c \n", ch1, ch2, ch3, ch5, ch4);

	return 0;
}
```

<br/>

예제 12

배열에 대한 설명 중 잘못된 것을 모두 고르시오.  
(1) 배열은 같은 데이터형의 변수를 여러 개 연속적으로 메모리에 할당하는 것이다.  
(2) 배열의 각 원소는 인덱스로 접근한다.  
(3) 배열의 크기는 변수로도 지정할 수 있다.  
(4) 배열의 크기는 상수로만 지정할 수 있다.  
(5) 배열은 항상 자동으로 0으로 초기화한다.  
(6) 배열의 이름은 배열의 시작 주소이다.  



<br/>

예제 13  

구조체에 대한 설명 중 잘못된 것을 모두 고르시오.  
(1) 구조체는 같은 데이터형의 변수를 여러 개 연속적으로 메모리에 할당하는 것이다.  
(2) 구조체는 서로 다른 데이터형의 변수들을 하나로 묶은 것이다.  
(3) 구조체 안에 멤버로 배열이나 포인터를 넣을 수 있다.  
(4) 구조체를 정의하면 메모리에 멤버가 할당된다.  
(5) 구조체는 사용자 정의형이다.  



<br/>

예제 14  

백화점의 고객관리 프로그램을 작성하려고 합니다.  
각 고객에 대한 정보로 이름, 나이, 성별, 주소, 전화번호 등을 저장하는 구조체를 정의하고, 구조체 변수를 하나 선언한 후 고객 정보를 입력받아 출력하는 프로그램을 작성해보세요.

<br/>

예제 15  

배열의 크기가 10인 임의의 1차원 배열을 초기화하고, 배열과 배열의 크기 10을 함수의 인자로 처리하여 배열 요소 전체의 합을 변환하는 함수를 작성하고 프로그램을 완성하라.
