# 7주차

내용: 동적 메모리 할당

<br/>

### 1. 포인터 복습 예제

<br/>

코드의 결과를 예상해보세요!  

예제 1

```c
#include <stdio.h>

int main()
{
	int a = 3;
	int *ap = &a;
	int b = 5;
	b = *ap;
	printf("%d\n", b);
}
```  


<br/>

예제 2

```c
#include <stdio.h>

int main()
{
	int x, y;
	int *xp = &x;
	int *yp = &y;
	int *tp;
	tp = yp;
	yp = xp;
	xp = tp;
	*xp = 5;
	*yp = 3;
	printf("%d\n", x);
	printf("%d\n", y);
}
```  

<br/>

예제 3

```c
#include <stdio.h>

int main()
{
	int a[4] = {1, 2, 3, 4};
	int *b = a;
	b++;
	printf("%d\n", b[0]);
}
```  

<br/>


예제 4  

```c
#include <stdio.h>

int main()
{
	int a[3] = {1, 2, 3};
	int *b = &(a[2]);
	*(b - a[0]) = 12;
	printf("%d, %d, %d\n", a[0], a[1], a[2]);
}
```

예제 5

```c
#include <stdio.h>

int main()
{
	int a[3] = {1, 2, 3};
	int b[3] = {1, 2, 3};
	int *c = b;
	c += 4;
	*c = 12;
	printf("%d, %d, %d\n", a[0], a[1], a[2]);
}
```

<br/>

코드를 직접 구현하세요!

예제 6  

삼각형의 밑변과 높이를 구조체를 이용하여 나타내고, 두 삼각형의 객체를 생성하여 넓이를 비교하는 함수를 구현하세요!  

  
예시 결과
```
삼각형 1
밑변 : 4
높이 : 5

삼각형 2
밑변 : 3
높이 : 7

삼각형 2의 넓이가 더 큽니다.
```  
  
정답 코드  
```c
#include <stdio.h>

// 삼각형 구조체 정의
struct Triangle {
    float base;
    float height;
};

// 삼각형의 넓이를 계산하는 함수
float calculateArea(struct Triangle triangle) {
    return 0.5 * triangle.base * triangle.height;
}

int main() {
    struct Triangle triangle1, triangle2;

    // 첫 번째 삼각형 정보 입력
    printf("삼각형 1\n");
    printf("밑변 : ");
    scanf("%f", &triangle1.base);
    printf("높이 : ");
    scanf("%f", &triangle1.height);

    // 두 번째 삼각형 정보 입력
    printf("\n삼각형 2\n");
    printf("밑변 : ");
    scanf("%f", &triangle2.base);
    printf("높이 : ");
    scanf("%f", &triangle2.height);

    // 넓이 비교
    float area1 = calculateArea(triangle1);
    float area2 = calculateArea(triangle2);

    if (area1 > area2) {
        printf("삼각형 1의 넓이가 더 큽니다.\n");
    } else if (area1 < area2) {
        printf("삼각형 2의 넓이가 더 큽니다.\n");
    } else {
        printf("두 삼각형의 넓이가 같습니다.\n");
    }

    return 0;
}
```

예제 7  
  
이름, 나이, 성적으로 구성된 학생 구조체를 만들고, 5명의 학생 구조체 배열을 생성합니다. 그리고 특정 성적을 입력받고, 그 성적보다 높은 성적을 가진 학생들을 모두 출력해보세요!

```
Student 1:
Enter name: Alice
Enter age: 20
Enter grade: 85.5

Student 2:
Enter name: Bob
Enter age: 21
Enter grade: 77.8

Student 3:
Enter name: Carol
Enter age: 22
Enter grade: 91.2

Student 4:
Enter name: David
Enter age: 20
Enter grade: 79.3

Student 5:
Enter name: Eve
Enter age: 21
Enter grade: 88.0

Enter the threshold grade: 80.0

Students with grade higher than 80.00:
Name: Alice, Age: 20, Grade: 85.50
Name: Carol, Age: 22, Grade: 91.20
Name: Eve, Age: 21, Grade: 88.00
```

### 2. 동적 메모리 할당

</br>

우리는 지금까지 `int a = 0` 이런 식의 메모리 할당을 사용해왔는데요, 이는 컴파일 과정에서 메모리를 할당해주는 것이라면, 우리가 이제부터 배울 것은 런타임 과정에서 메모리를 할당해주는 동적 메모리 할당입니다.  

프로그램이 실행 도중에 동적으로 메모리를 필요한 만큼의 메모리를 할당 받아서 사용한 뒤, 사용이 끝나면 메모리를 반납합니다.  메모리를 명시적으로 반납해주지 않으면, 메모리 누수가 발생하기 때문에, 동적 메모리의 사용이 끝나면 반드시 해당 메모리 영역을 반납해주어야 합니다.

c언어에서는 malloc()의 라이브러리 함수를 사용하여 동적으로 메모리를 할당받아 사용합니다. 참고로, c언어에서 동적 메모리 접근은 포인터를 통해서만 이루어집니다.

```c
// 동적 메모리 할당 방식
# include <stdio.h>
# include <stdlib.h>

int main() {
    int *a;
    a = (int *)malloc(sizeof(int)); // int의 크기만큼 메모리를 할당해라.
    *a = 100;
    printf("%d\n", *a);

    // a의 사용이 끝났다면 무조건 해당 메모리를 반납해야함.
    free(a);
    
    return 0;
}
```  

**의문점**
```c
int n;
scanf("%d", &n);
int arr[n];
```  
이런 식으로 가변 길이 배열을 이용하여 런타임 도중에 배열을 할당할 수 있는데, 굳이 동적 할당을 써야하나요?  
-> 배열의 크기가 작고, 스택 오버플로우가 발생하지 않을 것으로 예상되는 경우에는 가변 길이 배열을 사용하는 것이 효율적이지만, 배열의 크기가 크고, 실행 시간에 메모리 할당에 실패할 가능성이 있는 경우에는 동적 메모리 할당을 사용하는 것이 안전하고 유연합니다.  

굳이 따지자면, 가변 길이 배열은 자동적으로 메모리가 해제되지만, 동적으로 할당된 메모리는 프로그래머가 명시적으로 해제해주어야하기 때문에 더 불편합니다.

</br>

### 3. 대표적인 메모리 할당 3가지  

**malloc()**  

```c
int *ptr = (int *)malloc(10 * sizeof(int)); // int형 변수 10개의 메모리를 할당
```  

</br>

**calloc()**
```c
int *ptr = (int *)calloc(10, sizeof(int)); // int형 변수 10개의 메모리를 할당하고 0으로 초기화
```

</br>

**realloc()**
```c
int *ptr = (int *)malloc(10 * sizeof(int)); // int형 변수 10개의 메모리를 할당
ptr = (int *)realloc(ptr, 20 * sizeof(int)); // int형 변수 20개의 메모리로 재할당
```

</br>



### 4. 동적 할당 구현해보기!

**예제 1**  
학생의 수를 입력받고, 그 학생 수만큼 메모리를 동적으로 할당한 뒤, 평균을 구해보세요!  

예시 결과  
```
학생의 수 : 10

학생1: 20
학생2: 30
학생3: 10
학생4: 93
학생5: 57
학생6: 88
학생7: 84
학생8: 70
학생9: 40
학생10: 55

평균: 54
```


**예제 2**
양의 정수 n,m을 입력받고, 길이가 n인 int형 배열을 동적으로 할당한 뒤, 1~n까지 배열에 넣어서 출력하고, 해당 배열의 메모리를 해제합니다.  
그리고 같은 이름으로 char형 문자열을 m의 크기로 동적으로 할당한 뒤, 'a'를 m개 넣고, 출력해보세요!  

예시 결과
```
n : 4
m : 3

1 2 3 4 
aaa
```  


**예제 3**
이름, 나이, 성적으로 구성된 학생 구조체를 생성하고,  
학생의 수 n을 입력받은 뒤, 그 수만큼 구조체 배열의 메모리를 동적으로 할당하여  
학생들의 정보를 입력받고 검색 기능을 만든 뒤, 메모리를 해제해보세요!

Hint! - 동적으로 구조체 배열 할당하는 법  
`struct S *s = (struct S *)malloc(n * sizeof(struct S))`  

예시 결과
```
학생의 수 : 3

학생 1
이름 : 박진홍
나이 : 24
성적 : 80

학생 2
이름 : 홍길동
나이 : 25
성적 : 85

학생 3 
이름 : 박명수
나이 : 53
성적 : 70

검색할 학생의 이름 : 박명수
이름 : 박명수
나이 : 53
성적 : 70
```