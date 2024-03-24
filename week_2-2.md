# 2주차 - 추가 내용


### 주석

```c
// 이 내용은 컴파일 과정에서 완전히 무시됩니다.

/*
이 내용도 컴파일 과정에서 완전히 무시됩니다.
*/
```

<br/>

### main 함수 설명
```c
#include <stdio.h>

int main(void)
{
    printf("hello world\n");

    return 0;
}
```

<br/>

### 사용자 정의 함수
```c
#include <stdio.h>

void Hello_world(void)
{
    printf("hello world\n");
}

int main(void)
{
    Hello_world();

    return 0;
}
```

<br/>

### 자료형
(메모리는 운영체제마다 다를 수 있음)

**정수형**
|자료형|메모리|범위|
|----|---|---|
|short|2 byte|-32768 ~ 32767|
|int|4 byte|-2147483648 ~ 2147483647|
|long|4 byte|-2147483648 ~ 2147483647|
|unsigned short|2 byte|0 ~ 65535|
|unsigned int|4 byte|0 ~ 4294967295|
|unsigned long|4 byte|0 ~ 4294967295|

**문자형**
|자료형|메모리|범위|
|----|---|---|
|char|1 byte|-128 ~ 127|
|unsigned char|1 byte|0 ~ 255|

**부동소수점형**
|자료형|메모리|범위|
|----|---|---|
|float|4 byte|1.17549E-38 ~ 3.40282E38|
|double|8 byte|2.22507E-308 ~ 1.79769E308|

<br/>

**long형을 사용할 경우**
```c
long int num1 = 123456789L;
long num2 = 987654321l;
```

**unsigned를 사용할 경우**
```c
unsigned int num1 = 12345U;
unsigned num2 = 67890u;
```

**float형을 사용할 경우**
```c
float num1 = 123456789F;
float num2 = 987654321f;
```

<br/>

### #define
```c
#define MY_AGE 24
```

<br/>

### const
```c
const int MY_AGE = 24;
```

<br/>

### 변수 선언
```c
int n;

int n1, n2;
/* int n1; int n2;*/

int n = 10;
/* int n; n = 10; */

int n1 , n2 = 0;
/* int n1; int n2 = 0; */
```

<br/>

### 형식지정자

정수형

char : %c  

short : %hd  

int : %d  (8진수 : %o, 16진수 : %x)

long : %ld  

long long : %lld

<br/>

실수형

float : %f  

double : %lf  

long double : %Lf  

<br/>

문자열 : %s

<br/>

### 삼항연산자

A ? B : C

→ A가 참이면 B를 반환하고, A가 거짓이면 C를 반환

```c
#include <stdio.h>

int main(void)
{
	int x = -50, y = 30;
	int absX = (x > 0) ? x : -x; // x가 0보다 크면 x를 반환하고, x가 0보다 작으면 -x를 반환
	printf("x의 절댓값은 %d\n", absX);

	int max = (x > y) ? x : y;
	int min = (x < y) ? x : y;
	printf("x와 y 중 큰 값은 %d\n", max);
	printf("x와 y 중 작은 값은 %d\n", min);

	return 0;
}

/*
출력
x의 절댓값은 50
x와 y 중 큰 값은 30
x와 y 중 작은 값은 -50
*/
```

<br/>

### 형변환

1. 묵시적 변환
2. 자동 형 변환
3. 명시적 변환

<br/>

### 연산자 우선순위

<br/>

### switch 문

```c
switch (grade) {
	case 4:
		printf("훌륭해요!");
		break;
	case 3:
		printf("좋아요!");
		break;
	case 2:
		printf("평균이네요!");
		break;
	case 1:
		printf("좋지 않아요!");
		break;
	case 0:
		printf("좀 더 노력하세요!");
		break;
	default:
		printf("잘못된 학점입니다");
		break;
}
```