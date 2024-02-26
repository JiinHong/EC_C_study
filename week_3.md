# 3주차

내용 : 반복함수 & 재귀함수, 배열, 다차원 배열

<br/>

### 1. 반복함수

---

반복함수는 말 그대로 특정 기능을 반복하는 함수를 뜻합니다.

반복함수라는 말 자체는 별로 중요하지 않으니, 기능에 집중해주세요!

<br/>

### <특정 숫자를 입력한 횟수만큼 출력시키는 프로그램>

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

### <조합 프로그램 전체 코드>

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

<br/>

### 1. 배열(Array)

---

배열은 데이터가 많을 때 사용됩니다. 

데이터들의 집합을 표현할 수 있기 때문에 효과적이어서, 대부분의 프로그램에 사용됩니다!

```c
// 기본적인 선언은 다음과 같습니다.
int array[5];

// 배열을 선언함과 동시에 값을 넣어주고싶다면,
int array[] = {1, 2, 3, 4, 5};
// 다음과 같이 원하는 값들을 {}로 감싸서 넣어주면 됩니다.
```

<br/>

### <5개의 정수 중에서 최대값과 그 최대값의 인덱스를 출력하는 프로그램>

```c
#include <stdio.h>

int main(void)
{
	int max, index;

	// 크기가 5칸인 배열을 선언
	int array[5];

	max = 0;
	index = 0;

	for (int i = 0; i < 5; i++)
	{
		scanf("%d", &array[i]);
		if (max < array[i])
		{
			max = array[i];
			index = i;
		}
		// 크기가 5인 배열은 0번째, 1번째, 2번째, 3번째, 4번째 요소로 이루어집니다.
		// array[1]은 맨 처음의 요소가 아니라 array[0]의 다음 요소임을 명심하세요!
	}

	printf("해당 배열에서 가장 큰 값은 %d입니다. %d번째 인덱스에 위치합니다.\n", max, index);

	return 0;
}

/*
1 3 5 4 2
해당 배열에서 가장 큰 값은 5입니다. 그리고 2번째 인덱스에 위치합니다.
*/
```

<br/>

여기서 조금만 더 들어가서, 

### <5개의 정수 중 짝수 최대값과 홀수 최대값을 출력하는 프로그램>

```c
#include <stdio.h>

int main(void)
{
	int evenMax, oddMax;

	// 크기가 5칸인 배열을 선언
	int array[5];

	evenMax = 0;
	oddMax = 0;

	for (int i = 0; i < 5; i++)
	{
		scanf("%d", &array[i]);
		if (array[i] % 2 == 0) // 입력값이 짝수라면
		{
			if (evenMax < array[i]) // 입력값이 현재까지의 최대값보다 크다면
			{
				evenMax = array[i]; // 최대값 업데이트
			}
		}
		else // 입력값이 홀수라면
		{
			if (oddMax < array[i])
			{
				oddMax = array[i];
			}
		}
	}

	printf("해당 배열에서 짝수 최대값은 %d이고, 홀수 최대값은 %d입니다.\n", evenMax, oddMax);

	return 0;
}

/*
1 3 5 4 2
해당 배열에서 짝수 최대값은 4이고, 홀수 최대값은 5입니다.
*/
```
