# 2주차

내용: 기본입출력, 반복문, 조건문, 함수

조건문과 반복문은 논리흐름의 기본입니다.  
**조건문**은 조건에 따라 해당 코드가 실행되게 하는 것을 말합니다.  
**반복문**은 반복적으로 같은 코드를 반복하는 것을 말합니다.

<br/>

### 1. 조건문 & 반복문

---

### `<if>`

if문의 구조는 다음과 같습니다.

```c
if(조건)
{
// 조건이 참이라면, 코드를 실행
}
```

<br/>

if문을 이용하여 변수의 값을 절댓값으로 바꾸기

```c
#include <stdio.h>

int main(void)
{
	int x = -150;

	if(x < 0) // x가 0보다 작다면,
	{
		x = -x; // x의 부호를 바꿈
	}

	printf("x의 절댓값은 %d입니다.\n",x);

	return 0;
}

// 출력 : x의 절댓값은 150입니다.
```

<br/>

`<else if>`는 항상 if문 다음에 오는 조건문으로,  if문이 거짓(False)일 때 추가적인 조건을 검사하는데 사용됩니다. 예를 들어, 아래의 코드에서 score이 90 이상이 아니라면, 다음 else if문의 조건을 확인합니다.

점수에 따라 학점을 부여하는 프로그램

```c
#include <stdio.h>

int main(void)
{
	int score = 85;
	if (score >= 90) // score이 90 이상이면, {} 안의 코드 실행
	{
		printf("당신의 학점은 A입니다.\n");
	}
	else if (score >= 80) // score이 90점 이상이 아니고, 80점 이상이면, {} 안의 코드 실행
	{
		printf("당신의 학점은 B입니다.\n");
	}
	else if (score >= 70)
	{
		printf("당신의 학점은 C입니다.\n");
	}
	else if (score >= 60)
	{
		printf("당신의 학점은 F입니다.\n");
	}

	return 0;
}

// 출력 : 당신의 학점은 B입니다.
```

<br/>

윤년 판독 프로그램

윤년 : 4년마다, 2월이 29일로 늘어나는 해

윤년은 4년마다 오지만, 100년 단위일 때는 윤년에 해당하지 않고, 400년 단위일 때는 무조건 윤년에 해당되는 것이 세계표준입니다.

2024년은 4로 나누어 떨어지고, 100년 단위가 아니므로 윤년이 됩니다.

```c
#include <stdio.h>

int main(void)
{
	int year = 2024;
	// (4로 나누어 떨어지면서 100으로는 나누어 떨어지지 않아야함) or (400으로 나누어 떨어져야함)
	if((year % 4 == 0 && year % 100 != 0) || year % 400 == 0)
	{
		printf("%d년은 윤년입니다.\n",year);
	}
	else
	{
		printf("%d년은 윤년이 아닙니다.\n", year);
	}

	return 0;
}

/*
출력
2024년은 윤년입니다.
*/
```

<br/>

### `<while>`

while문은 조건이 True일 경우, 계속해서 반복하는 문법입니다. 계속 True라면, 코드를 무한반복합니다.

while문의 구조는 다음과 같습니다.

```c
while(조건)
{
	// 조건에 만족하는 한, 해당 코드를 계속 반복
}
```

<br/>

1부터 1000까지 더하기

```c
#include <stdio.h>

int main(void)
{
	int i = 1, sum = 0;
	while(i<=1000) // i가 1000 이하이면, 계속 반복
	{
		sum += i;
		i++; // 반복될 때마다 i에 1을 더함
	}
	printf("1부터 1000까지의 합은 %d입니다.\n",sum);
	
	return 0;
}
```

<br/>

### `<for>`

for문은 정해진 횟수만큼 코드를 반복해야할 때 쓰입니다.

일단, 구조는 다음과 같습니다.

```c
for(초기화식; 조건식; 증감식)
{
	// 조건식이 만족하면 해당 코드를 실행한 뒤, 증감식을 수행함.
}
```

<br/>

### 별 10개 출력하기

```c
#include <stdio.h>

int main(void)
{
	for(int i = 0; i < 10; i++)
	{
		printf("*");
	}

	// for문의 실행 순서
	// (1) i값을 0으로 초기화한다.
	// (2) i가 10 미만이면, {}안의 코드를 실행한 뒤, i++을 한다.
	// (3) (2)의 과정을 반복한다.

	return 0;
}

// 출력 : **********
```

<br/>

### 별 100개 출력하기

```c
#include <stdio.h>

int main(void)
{
	for(int i = 0; i < 10; i++)
	{
		for(int j = 0; j < 10; j++)
		{
			printf("*");
		}
		printf("\n");
	}

	return 0;
}

/*
출력
**********
**********
**********
**********
**********
**********
**********
**********
**********
**********
*/
```

<br/>

### 피라미드 출력하기(조금 어려울 수 있습니다. 이해해보세요!)

```c
#include <stdio.h>

int main(void)
{
	for(int i = 0; i < 10; i++)
	{
		for(int j = 10 - i; j > 0; j--) // 공백을 10 - i만큼 출력
		{
			printf(" ");
		}
		for(int j = 2*i + 1; j > 0; j--) // "*"을 2*i + 1만큼 출력
		{
			printf("*");
		}
		printf("\n"); // 반복 한 번이 끝나면 줄넘김
	}

	return 0;
}

/*
출력
          *
         ***
        *****
       *******
      *********
     ***********
    *************
   ***************
  *****************
 *******************
*/
```

<br/>

### <알아두어야 할 것들!>

- 0이 아닌 모든 수는 참으로 분류됩니다.
- for(;;)와 while(1)은 무한루프로 동작합니다.

```c
for(;;) // 이는 조건식이 비어있으므로, 아무 조건없이 계속 반복한다는 의미입니다
{
	printf("*"); // "*"을 무수히 출력
}
```

- break;는 반복문을 즉시 탈출합니다.

```c
#include <stdio.h>

int main(void)
{
	int a = 0;
	while (1)
	{
		if (a == 3)
		{
			break;
		}
		printf("%d", a);
		a++;
	}
	return 0;
}

/*
출력
012
*/
```

<br/>

### 2. 기본 입출력

---

### <scanf>

scanf는 사용자에게 입력을 받는 문법입니다.

구조는 scanf(”%d”, &x);와 같습니다.

%d에 해당하는 값을 **&x**에 넣는다는 의미입니다. &x란, x라는 변수의 메모리 주소를 의미합니다.

정수를 받고싶다면 %d, 문자를 받고싶다면 %c, 실수를 받고싶다면 %f 등의 다양한 문법을 사용하여 입력받아야합니다.

```c
#include <stdio.h>

int main(void)
{
	int x;
	scanf("%d", &x); // 사용자가 입력한 수를 x에 넣음
	printf("당신이 입력한 값은 %d입니다.\n", x);

	return 0;
}

/*
입력
123

출력
당신이 입력한 값은 123입니다.
*/
```

<br/>

### <간단한 계산기 만들어보기>

```c
#include <stdio.h>

int main(void)
{
	char o;
	int x, y;
	while (1)
	{
		printf("수식을 입력하세요 : ");
		scanf("%d %c %d", &x, &o, &y);

		if (o == '+')
		{
			printf("%d %c %d = %d\n", x, o, y, x + y);
		}
		else if (o == '-')
		{
			printf("%d %c %d = %d\n", x, o, y, x - y);
		}
		else if (o == '*')
		{
			printf("%d %c %d = %d\n", x, o, y, x * y);
		}
		else if (o == '/')
		{
			printf("%d %c %d = %d\n", x, o, y, x / y);
		}
		else if (o == '%')
		{
			printf("%d %c %d = %d\n", x, o, y, x % y);
		}
		else
		{
			printf("입력이 잘못되었습니다.\n");
		}

		getchar();
		// c언어에서는 enter도 하나의 문자로 인식하기 때문에
		// getchar을 이용하여 버퍼를 처리해줍니다. 즉, enter(줄넘김)을 처리합니다.

		printf("프로그램을 종료하시겠습니까? (y/n) ");
		scanf("%c",&o);
		if(o == 'n' || o == 'N')
		{
			continue; 
			// continue는 아래의 코드를 실행하지 않고, 다시 while문의 첫부분으로 돌아간다는 의미입니다
		}
		else if(o == 'y' || o == 'Y')
		{
			break; // while문을 탈출
		}
		else
		{
			printf("입력이 잘못되었습니다.\n");
		}
	}

	return 0;
}
```

<br/>

### <입력한 횟수만큼 정수를 더하는 프로그램>

```c
#include <stdio.h>

int main(void)
{
	int n, x, sum = 0;
	printf("덧셈 횟수를 입력하세요 : ");
	scanf("%d", &n);

	for(int i = 0; i < n; i++)
	{
		// 정수를 입력받고, 그 정수를 sum에 계속 더함
		printf("덧셈할 정수을 입력하세요 : ");
		scanf("%d",&x);
		sum += x;
	}

	printf("결과 : %d\n", sum);
	return 0;
}

/*
덧셈 횟수를 입력하세요 : 3
덧셈할 정수을 입력하세요 : 1
덧셈할 정수을 입력하세요 : 2
덧셈할 정수을 입력하세요 : 3
결과 : 6
*/
```

<br/>

### <구구단의 특정 단을 출력하는 프로그램>

```c
#include <stdio.h>

int main(void)
{
	int x;
	printf("출력할 단을 입력하세요 : ");
	scanf("%d", &x);

	for(int i = 1; i<=9; i++)
	{
		printf("%d X %d = %d\n", x, i, x*i);
	}

	return 0;
}

/*
출력할 단을 입력하세요 : 7
7 X 1 = 7
7 X 2 = 14
7 X 3 = 21
7 X 4 = 28
7 X 5 = 35
7 X 6 = 42
7 X 7 = 49
7 X 8 = 56
7 X 9 = 63
*/
```

<br/>

### 2. 사용자 정의 함수 (Function)

특정한 기능을 수행하는 함수를 직접 만들어서 하나의 문제를 잘게 분해할 수 있습니다. 이렇게 사용자 정의 함수를 만들어서 사용하면 작업의 효율을 높일 수 있습니다.

<br/>

### <시간 더하기 프로그램>

특정한 시간에 x분을 더하면 몇 시 몇 분이 되는지 알려주는 프로그램입니다.

```c
#include <stdio.h>

// 전역 변수 선언
int hour, minute, minuteAdd;

int counter()
{
	minute += minuteAdd;
	hour += minute / 60;
	minute %= 60;
	hour %= 24;
}

int main(void)
{
	printf("현재의 시를 입력하세요 : ");
	scanf("%d",&hour);
	printf("현재의 분을 입력하세요 : ");
	scanf("%d",&minute);
	printf("더할 분을 입력하세요 : ");
	scanf("%d",&minuteAdd);
	counter();
	printf("더해진 시간은 %d시 %d분입니다.\n",hour,minute);
	return 0;
}

/*
현재의 시를 입력하세요 : 12
현재의 분을 입력하세요 : 50
더할 분을 입력하세요 : 30
더해진 시간은 13시 20분입니다.
*/
```

<br/>

### <특정한 금액을 입력 받고, 해당 금액에서 화폐의 개수를 가장 적게 주는 프로그램>

```c
#include <stdio.h>

// int minimum에서 int는 return할 값의 형태가 int형이라는 의미입니다.
// 여기서 int money를 매개변수(파라미터)라고 하는데, 
// 함수 내부에서 쓰일 값들을 선언해서, 입력받기 위해서 존재합니다.
// 아래의 예시에서는 화폐의 개수를 셀 금액을 입력받고 있습니다.
int minimum(int money)
{
	int count = 0;
	while (money >= 50000) // 5만원보다 크면 
	{
		money -= 50000; // 5만원씩 빼가면서 화폐의 개수 세기
		count += 1;
	}
	while (money >= 10000)
	{
		money -= 10000;
		count += 1;
	}
	while (money >= 5000)
	{
		money -= 5000;
		count += 1;
	}
	while (money >= 1000)
	{
		money -= 1000;
		count += 1;
	}

	return count;
}

int main(void)
{
	int input;
	printf("금액을 입력하세요 : ");
	scanf("%d",&input);
	printf("%d\n",minimum(input));

	return 0;
}

/*
금액을 입력하세요 : 66000
4
(5만원짜리 하나, 만원짜리 하나, 오천원짜리 하나, 천원짜리 하나, 총 4개)
*/
```

<br/>

### <1월 1일부터 며칠이 지났는지 알려주는 프로그램>

```c
#include <stdio.h>

// 이 함수는 윤년을 감안하지 않습니다.
// 현재 날짜를 매개변수로 넣어주기
int getDays(int month, int day)
{
	int i, sum = 0;
	
	// 전 달까지의 일수를 더해주기
	for (i = 1; i < month; i++)
	{
		if (i == 2)
		{
			sum += 28;
		}
		else if (i % 2 == 0 && i < 8) // 7월까지는 짝수 달이 30일
		{
			sum += 30;
		}
		else if (i % 2 == 1 && i > 8) // 9월부터는 홀수 달이 30일
		{
			sum += 30;
		}
		else
		{
			sum += 31;
		}
	}
	return sum + day;
}

int main(void)
{
	int month, day;
	printf("몇 월인지 입력하세요 : ");
	scanf("%d", &month);
	printf("며칠인지 입력하세요 : ");
	scanf("%d", &day);

	printf("오늘은 %d일째입니다.\n", getDays(month,day));

	return 0;
}

/*
몇 월인지 입력하세요 : 3
며칠인지 입력하세요 : 1
오늘은 60일째입니다.
*/
```

<br/>

### 이제 solved.ac CLASS 1 달성하러 가봅시다!
https://solved.ac/class?class=1  
-> 1000, 1001, 1008, 10998, 1330, 2475, 2557, 2753, 9498, 10869, 11654  
-> 10950, 10951, 10952, 2438, 2439  
-> 15894, 2441, 2442, 2754, 4153

배열 학습 뒤
-> 2525, 2562, 5597

<br/>

### Visual Studio에서 scanf 오류 해결

코드의 맨 위에 아래의 코드를 적어주시면 보안 오류가 안생깁니다!
```c
#define _CRT_SECURE_NO_WARNINGS
```