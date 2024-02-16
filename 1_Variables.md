# 1주차


### 1. Hello World!

---

무작정 따라해보세요! 하나도 이해가 가지 않아도 됩니다. 어차피 뒤에서 다 배우게 됩니다!!

```c
#include <stdin.h>

int main(void)
{
	printf("Hello World");
	return 0;
}
```

#include <stdio.h> : 기본입출력 함수를 제공해주는 라이브러리 호출

int main() : main이라는 함수 호출, 그리고 그 함수의 반환값을 int형으로 지정

printf() : 사용자에게 '출력'기능을 제공해주는 기본적인 함수

return : 하나의 함수가 종료될 때, 반환값을 지정해주는 문법

C언어에서 main 함수는 파일이 실행되면 가장 먼저 실행되는 함수로 약속되어있습니다.

<br/>

### 2. 변수

---

**Variables** : 변수

**변수 선언해보기! (자료형 선언)**

```c
#include <stdio.h>

int main(void)
{
	int x; // 정수 선언
	x = 3;
	printf("x : %d \n",x);
	printf("x의 메모리 용량은 %d \n",sizeof(x));

	float y; // 실수 선언
	y = 123456789.123456789; 
	printf("y : %f \n",y); // 정상적으로 출력되지않음 (출력값 : 123456792.000000)
	printf("y의 메모리 용량은 %d \n",sizeof(y));

/*
float 자료형은 4바이트까지밖에 담을 수 없기 때문에
double 자료형을 이용해야한다
*/

	double z; // 실수 선언
	z = 123456789.123456789;
	printf("z : %f \n",x);
	printf("z의 메모리 용량은 %d \n",sizeof(z));

	return 0;
}
```

다음은 자료형의 메모리 크기입니다. 지금 외우실 필요 전혀없고, ‘그냥 그렇구나~’ 해주세요!

<br/>

정수형

char : 1 byte

short : 2 byte

int : 4 byte

long : 4 byte

long long : 8 byte  

<br/>

실수형

float : 4 byte

double : 8 byte

long double : 8 byte

<br/>

그렇다면 int형의 최댓값과 최솟값은?

```c
#include <stdio.h>
#include <limits.h>

int main(void)
{
	int x = LONG_MAX;
	printf("int형의 최댓값 x는 %d \n", x); // 출력값 : 2147483647 (약 21억)
	
	// 여기서 1을 더하면 어떻게 될까?
	printf("int형의 최댓값 x에 1을 더하면? %d \n", x+1); // 출력값 : -2147483648

	/*
	int형이 가질 수 있는 최댓값을 넘어가면,
	오히려 최솟값으로 돌아가게 됩니다.
	이 현상을 오버플로우(overflow)라고 합니다.
	*/

	return 0;
}
```

<br/>

<간단한 사칙연산>

```c
#include <stdio.h>

int main(void)
{
	int x = 3;
	int y = 5;
	printf("x = %d \n", x);
	printf("y = %d \n", y);
	printf("x + y = %d \n", x + y);
	printf("x - y = %d \n", x - y);
	printf("x * y = %d \n", x * y);
	printf("x / y = %d \n", x / y); // 몫만 출력
	printf("x / y = %d \n", x % y); // 나머지만 출력

	// 실제 나눈 값을 알고 싶다면, 연산을 실수형으로 수행해야합니다.
	printf("x / y = %f \n", (double)x / y); // 실제 나눈 값
	return 0;
}
```
