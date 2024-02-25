# 3주차

내용 : 반복함수 & 재귀함수, 배열, 다차원 배열

<br/>

### 1. 반복함수

---

반복함수는 말 그대로 특정 기능을 반복하는 함수를 뜻합니다.

반복함수라는 말 자체는 별로 중요하지 않으니, 기능에 집중해주세요!

<br/>

<특정 숫자를 입력한 횟수만큼 출력시키는 프로그램>

```c
#include <stdio.h>

// a만큼 출력을 반복하는 함수

// 리턴값이 없으므로 함수의 리턴형식은 void로 해줍니다.
void repeat(int a)
{
	for (int i = 0; i<a; i++) // i가 a와 같아질 때까지 반복, 즉 a만큼 반복
	{
		printf("hi ");
	}
}

int main(void)
{
	int x;
	printf("출력할 횟수를 입력하세요 : ");
	scanf("%d", &x);
	repeat(x);

	return 0;
}

/*
출력할 횟수를 입력하세요 : 5
hi hi hi hi hi
*/
```

<br/>

### 1. 재귀함수 (Recursive Function)

---

재귀함수는 함수 안에 같은 함수를 넣어서 함수 내부에서 자기자신을 재귀적으로 실행하는 함수입니다.

위에서의 프로그램과 같은 프로그램을 재귀함수로 만들기

```c
#include <stdio.h>

// a만큼 출력 반복하기
void repeat(int a) // 리턴값이 없으므로 함수의 리턴형식은 void로 해줍니다.
{
	// 종료 조건을 먼저 명시해주기
	if (a == 0)
	{
		return;
	}

	// 종료 조건이 False인 경우, 계속 hi를 출력
	printf("hi ");

	//a를 -1해가며 재귀적으로 자기자신을 호출
	repeat(a-1);
}

int main(void)
{
	int x;
	printf("출력할 횟수를 입력하세요 : ");
	scanf("%d", &x);
	repeat(x);

	return 0;
}

/*
출력할 횟수를 입력하세요 : 5
hi hi hi hi hi
*/
```

<br/>

재귀함수를 이용하여 조합(Combination) 구현하기

nCr의 공식

1. r이 0이거나 r이 n이면, 1이며,
2. (n-1)C(r-1) + (n-1)Cr 과 같다.

위의 공식을 함수로 만들어보면,

```c
int nCr(int n, int r)
{
	// r이 0이거나 n이면, 1을 리턴
	if(r == 0 || r == n)
	{
		return 1;
	}

	// nCr 공식을 그대로..
	return nCr(n-1, r-1) + nCr(n-1, r);
}
```

<br/>

<조합 프로그램 전체 코드>

```c
#include <stdio.h>

int nCr(int n, int r)
{
	// r이 0이거나 n이면, 1을 리턴
	if(r == 0 || r == n)
	{
		return 1;
	}

	// nCr 공식을 그대로..
	return nCr(n-1, r-1) + nCr(n-1, r);
}

int main(void)
{
	int n, r;
	printf("n을 입력하세요 : ");
	scanf("%d", &n);
	printf("r 입력하세요 : ");
	scanf("%d", &r);

	printf("%dC%d의 값은 %d입니다.\n", n, r, nCr(n,r));

	return 0;
}

/*
n을 입력하세요 : 5
r 입력하세요 : 3
5C3의 값은 10입니다.
*/
```
