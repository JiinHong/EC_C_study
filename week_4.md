# 4주차

내용: 포인터

<br/>

### 1. 포인터

포인터란 메모리의 주소값을 가리키는 변수입니다.  
C언어의 가장 큰 특징이자 장점이고, 중요한 개념이기 때문에 잘 이해하고 있어야합니다.

<br/>

기본적인 개념은 다음과 같습니다.

```c
int *y = &x;
// &는 주소를 의미하며, *는 주소값을 저장할 포인터 변수를 의미합니다.
// 즉, y라는 포인터 변수에 x의 주소를 넣는 것입니다.
// 그래서 포인터 y를 통해 x로 즉시 접근할 수 있어서,
// 값을 처리할 때 유용합니다.
```

<br/>

대표적인 포인터 사용 예시입니다.

### <두 변수의 값을 서로 변환하기>

```c
#include <stdio.h>

void swap(int *x, int *y)
{
	int temp;
	temp = *x; // x의 값을 temp에 넣기
	*x = *y; // x가 가리키는 값을 y가 가리키는 값으로 바꿈
	*y = temp; // y가 가리키는 값에 temp를 넣어주기
}

int main(void)
{
	int x = 1;
	int y = 2;
	swap(&x,&y); // 매개변수로 x의 주소와 y의 주소를 넣어주기
	printf("x = %d\ny = %d\n", x, y);

	return 0;
}

/*
x = 2
y = 1
*/
```

<br/>

위의 코드를 조금 더 분석해보면,

```c
#include <stdio.h>

void swap(int *x, int *y)
{
	int temp;
	temp = *x; // x의 값을 temp에 넣기
	*x = *y; // x가 가리키는 값을 y가 가리키는 값으로 바꿈
	*y = temp; // y가 가리키는 값에 temp를 넣어주기
	printf("*x : %d\n", *x);
	printf("*y : %d\n", *y);
	printf("temp : %d\n", temp);
	printf("&x : %d\n", &x);
	printf("&y : %d\n", &y);
	printf("&temp : %d\n", &temp);
}

int main(void)
{
	int x = 1;
	int y = 2;
	swap(&x,&y); // 매개변수로 x의 주소와 y의 주소를 넣어주기
	printf("x = %d\ny = %d\n", x, y);

	return 0;
}

/*
*x : 2
*y : 1
temp : 1
&x : 1864773000
&y : 1864772992
&temp : 1
x = 2
y = 1
*/
```

포인터라는 개념은 명칭 그대로 ‘가리킨다’를 의미합니다. 일종의 화살표라고 생각하면 됩니다.

예를 들어, *x는 ‘1864773000’라는 주소를 가리키는 것이고, 그 주소에 위치한 변수의 값이 2가 되는 것입니다.

포인터는 주소를 이용하기 때문에, 어느 함수에서든 포인터를 이용하여 그 값에 접근하기 때문에 특정 부분의 영향에 받지 않고, 메모리 자체에 접근할 수 있다는 점에서 C언어의 큰 무기입니다.

<br/>

아래의 코드로 포인터의 개념을 한번에 명확하게 설명드리겠습니다.

```c
#include <stdio.h>

int main(void)
{
	int *ptr;
	int a = 10;
	ptr = &a;

	printf("a : %d\n",a);
	printf("*ptr : %d\n", *ptr);
	printf("&a : %d\n", &a);
	printf("ptr : %d\n", ptr);

	// 즉, a는 *ptr와 같고,
	// &a는 ptr과 같습니다.

	// 그렇다면, ptr 자체는 어디에 저장될 까요?
	printf("&ptr : %d\n", &ptr);
	// 출력된 것처럼 또 다른 메모리에 저장됩니다!

	// 여기서 포인터를 이용하여 a의 값을 20으로 바꿔보세요!
	*ptr = 20; // 직접 메모리에 접근하여 값을 변경합니다
	printf("변경된 a : %d\n", a);	

	return 0;
}

/*
a : 10
*ptr : 10
&a : 1806970284
ptr : 1806970284
&ptr : 1806970288
변경된 a : 20
*/
```

<br/>

### 2. 문자열

문자열(String)은 메모리에 저장된 연속된 문자(char)들의 집합을 의미합니다.

큰따옴표(””)를 사용하여 표현되며, 아래의 예시처럼 선언하면 됩니다.

```c
#include <stdio.h>

int main(void)
{
	char str1[7] = "JinHong";
    // []안에는 문자열의 크기가 들어갑니다
    // 문자열의 크기를 자동으로 지정되게 하고싶으면 아래처럼 크기 적는 칸을 비워주면 됩니다.
	char str2[] = "My name is JinHong";

    printf("%s\n",str1);
    printf("%s\n",str2);
}

/*
JinHong
My name is JinHong
*/
```

<br/>

### <사용자에게 문자를 입력받아서 그 문자열의 글자수 세기>

```c
#include <stdio.h>

int main(void)
{
    char input[1001]; // 메모리의 크기가 1001인 문자열 선언
    gets(input); 
    // gets() 함수는 사용자에게 문자를 받아서 해당 변수에 넣는 함수입니다.
    // 남는 칸들은 모두 빈값(\0)으로 채워집니다.
    int count = 0;

    // count 변수를 +1 해가면서 빈값(\0)이 나오면 while문 탈출
    while (input[count] != '\0')
    {
        count++;
    }
    
    printf("입력한 문자열의 길이는 %d입니다.\n",count);
    printf("입력한 문자열은 %s입니다.\n",input);
    return 0;
}

/*
hello
입력한 문자열의 길이는 5입니다.
입력한 문자열은 hello입니다.
*/
```