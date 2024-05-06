# 6주차

내용: 구조체

<br/>

### 1. 포인터 복습 예제

<br/>

코드의 결과를 예상해보세요!  

예제 1

```c
#include <stdio.h>

int main() {
    int list[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
    int *p;
    p = list;
    printf("%d ", *list);
    printf("%d ", *p+3);
    printf("%d ", *(p+1));
}
```  


<br/>

예제 2

```c
#include <stdio.h>

int main(){
    int x = 6;
    int *p = &x;
    printf("%d ", --(*p));
    printf("%d ", (*p)++);
}
```  

<br/>

예제 3

```c
#include <stdio.h>

int main(){
    char *p;
    char s[] = "hello";
    p = s + strlen(s) - 1;
    while(p >= s) {
    printf("%s\n ", p);
    p--;
    }
}
```  

<br/>


예제 4  

```c
#include <stdio.h>

int main() {
    char str[] = "abcdefghij";
    char *p = NULL;
    int i;
    p = str + 3;
    for(i=0; i<3; i++, p++) {
    *p = '2' + i;
    }
    printf("str = %s", str);
}
```


### 2. 구조체

</br>

우리는 같은 타입의 변수들의 집합을 배열로 묶을 수 있었습니다. 이와 다르게, 다른 타입의 변수들을 묶을 수 있는 것이 바로 구조체입니다. 구조체의 선언 방식은 다음과 같습니다.  

```c
/*
struct 구조체이름
{
    멤버변수1의타입(ex. int) 멤버변수1의이름;
    멤버변수2의타입(ex. char) 멤버변수2의이름;
    ...
}
*/

// 예를 들어, book이라는 구조체를 선언한다고 하면, 
struct book
{
    char title[30];
    char author[30];
    int price;
};
```  

이렇게 제목과 저자, 가격의 형태로 구성된 틀을 이용하여, 다양한 책을 만들 수 있는 겁니다!  
붕어빵으로 비유를 하자면, book이라는 붕어빵 틀을 만들고, 각 책의 제목, 저자, 가격에 따라 찍어내는 느낌으로 생각하시면 됩니다!  

</br>

**구조체의 두 가지 초기화 방식**

```c
#include <stdio.h>
#include <string.h>

struct Score {
    char name[20]; //이름
    int kor; //국어성적
    int mat; //수학성적
    int eng; //영어성적
};

int main()
{
    //초기화 방법 (1) -> 선언시 바로 초기화
    struct Score s1 = { "홍길동",50,70,80 };
    
    //초기화 방법 (2) -> 선언후 .을 활용하여 초기화
    struct Score s2;
    strcpy(s2.name, "홍길동");
    s2.kor = 60;
    s2.mat = 70;
    s2.eng = 80;

    return 0;
}
```
위의 코드처럼, 중괄호를 통해 한꺼번에 초기화시켜주는 방식과, 각각의 요소에 "."을 이용하여 접근한 뒤 초기화시켜주는 방식이 있습니다.  


</br>

구조체를 이용하여 책을 표현한 코드  
```c
#include <stdio.h>
#include <string.h> //strcpy

struct Book {
    char title[30];
    char author[30]; // char * author; 로 해도되지만, 동적할당을 이용해야할 수 있음.
    int price;
}; // <- 세미콜론 넣어야함

int main() {
    struct Book book1;
    strcpy(book1.title, "Harry Potter"); // 문자열을 대입할 때 strcpy 함수 사용
    strcpy(book1.author, "J.K. Rowling");
    book1.price = 20000;

    struct Book book2;
    strcpy(book2.title, "The Great Gatsby");
    strcpy(book2.author, "F. Scott Fitzgerald");
    book2.price = 15000;

    // 위의 코드를 이렇게 한 줄씩으로 표현 가능
    // struct Book book1 = {"Harry Potter", "Rowling", 20000};
    // struct Book book2 = {"The Great Gatsby", "F. Scott Fitzgerald", 15000};

    printf("Book 1\n");
    printf("Title: %s\n", book1.title);
    printf("Author: %s\n", book1.author);
    printf("Price: %d\n\n", book1.price);

    printf("Book 2\n");
    printf("Title: %s\n", book2.title);
    printf("Author: %s\n", book2.author);
    printf("Price: %d\n", book2.price);

    return 0;
}
```  

위의 코드처럼 Book이라는 틀을 만들고, 다양한 책을 만들어낼 수 있습니다!  
그리고 book1.title처럼, book1의 title의 접근 하기 위해서는 "."을 이용합니다!  

</br>


### 3. 중첩 구조체

```c
#include <stdio.h>
 
// 과학
struct Science{
	char one[30];
    char two[30];
};

// 수학
struct Math{
	char one[30];
    char two[30];
};

struct Student{
    char name[30];
    int grade;
    struct Science s;
    struct Math m;
};

int main(){
	struct Student s1 = {"박진홍", 3, {"물리학", "지구과학"}, {"미적분", "확률과통계"}};
    struct Student s2 = {"홍길동", 2, {"화학", "생명과학"}, {"수학2", "미적분"}};
	
	printf("%s은 %d학년이며, 과목은 %s, %s입니다.\n", s1.name, s1.grade, s1.s.one, s1.s.two);
	printf("학생 정보\n");
    printf("--------\n");
    printf("이름: %s\n", s1.name);
    printf("학년: %d\n", s1.grade);
    printf("과학 과목: %s, %s\n", s1.s.one, s1.s.two);
    printf("수학 과목: %s, %s\n", s1.m.one, s1.m.two);
    printf("\n");
    printf("이름: %s\n", s2.name);
    printf("학년: %d\n", s2.grade);
    printf("과학 과목: %s, %s\n", s2.s.one, s2.s.two);
    printf("수학 과목: %s, %s\n", s2.m.one, s2.m.two);
	
	return 0;
}
```  

이런 식으로 중첩 구조체를 이용하여 다양한 방식으로 구조체를 설계할 수 있습니다.  
Math와 Science라는 구조체를 먼저 만들고, Student라는 구조체 안에 선언해주면 됩니다.

</br>

### 4. 구조체 배열

다음과 같이 구조체를 배열로 선언할 수도 있습니다.

```c
#include <stdio.h>
#include <string.h>

struct Score {
    char name[20]; // 이름
    int kor; // 국어성적
    int mat; // 수학성적
};

int main()
{
    struct Score s[3] = { 0 };

    // 학생 정보 입력
    printf("학생 정보를 입력하세요:\n");
    for (int i = 0; i < 3; i++) {
        printf("학생 이름: ");
        scanf("%s", s[i].name);
        printf("국어 성적: ");
        scanf("%d", &s[i].kor);
        printf("수학 성적: ");
        scanf("%d", &s[i].mat);
    }

    // 입력된 학생 정보 출력
    printf("\n입력된 학생 정보:\n");
    printf("----------------------------\n");
    for (int i = 0; i < 3; i++) {
        printf("이름: %s\n", s[i].name);
        printf("국어: %d\n", s[i].kor);
        printf("수학: %d\n", s[i].mat);
        printf("--------------------\n");
    }
    
    return 0;
}
```  

위와 같이 구조체를 배열로 만들고 사용할 수 있습니다.  
수많은 학생들의 수학 성적과 국어 성적을 구조체 배열을 통해 편하게 관리할 수 있습니다!

</br>

### 5. 구조체 예제 풀어보기~

**예제 1**  
4명의 이름과 전화번호를 저장하는 구조체 배열을 만들어 값을 저장한 후, 이름으로 검색하면 전화번호를 출력하는 프로그램을 작성해보세요.  

예시 결과
```c
1번째 사람 이름 : 홍길동
1번째 사람 전화번호 :1111

2번째 사람 이름 : 김민수
2번째 사람 전화번호 :2222

3번째 사람 이름 : 이영희
3번째 사람 전화번호 :3333

4번째 사람 이름 : 박명수
4번째 사람 전화번호 :44444

검색할 이름을 입력하세요 : 이영희
이름 : 이영희    전화번호: 3333 
```

정답 코드  
```c
#include <stdio.h>
#include <string.h>

struct Data {
	char name[10];
	char phone_number[15];
};

int main()
{
	const int N = 4;

	struct Data person[N];

	for (int i = 0; i < N; i++) {
		printf("%d번째 사람 이름 : ", i+1); 
        scanf("%s", person[i].name);
		printf("%d번째 사람 전화번호 :", i+1); 
        scanf("%s", person[i].phone_number);
		printf("\n");
	}

	char name[10];

	printf("검색할 이름을 입력하세요 : "); 
    scanf("%s", name);

	for (int i = 0; i < N; i++) {
		if (!(strcmp(person[i].name, name))) {
			printf("이름 : %s \t 전화번호: %s \n", person[i].name, person[i].phone_number);
		}
	}
}
```

<br/>

**예제 2**  
좌표평면의 x좌표와 y좌표를 구조체를 이용하여 나타내고, 2개의 점을 생성하여 피타고라스의 정리로 두 점 사이의 거리를 출력하는 코드를 작성해보세요! (두 점 사이의 거리를 계산하는 함수도 만들어야합니다~)

결과 예시
```c
첫 번째 점의 좌표(x y): 3 5
두 번째 점의 좌표(x y): 1 7
두 점 사이의 거리: 2.83
```

```c
#include <stdio.h>
#include <math.h>

struct Point {
    int x; // x 좌표
    int y; // y 좌표
};

// 두 점 사이의 거리 계산
double distance(struct Point p1, struct Point p2) {
    return sqrt(pow(p2.x - p1.x, 2) + pow(p2.y - p1.y, 2));
}

int main() {
    struct Point p1, p2; // 점 2개 생성

    printf("첫 번째 점의 좌표(x y): ");
    scanf("%d %d", &p1.x, &p1.y);

    printf("두 번째 점의 좌표(x y): ");
    scanf("%d %d", &p2.x, &p2.y);

    double dist = distance(p1, p2);

    printf("두 점 사이의 거리: %.2f\n", dist);

    return 0;
}
```

<br/>

**예제 2**  

프로그램 사용자로부터 이름과 나이를 다음의 형식에 맞춰서 입력받고, 두 사람의 이름과 나이가 같은지 다른지 판단하여 출력하는 프로그램을 작성해보세요!

예시 결과
```c
첫 번째 사람 정보 입력: 홍길동 22
두 번째 사람 정보 입력: 홍길동 33
이름이 동일합니다.
나이가 같지 않습니다.
```  

정답코드
```c
#include <stdio.h>
#include <string.h>

// 사용자 정보를 담는 구조체 정의
struct Person {
    char name[20]; // 이름
    int age; // 나이
};

int main() {
    // 두 명의 사용자 정보를 담을 구조체 변수 선언
    struct Person person1, person2;

    printf("첫 번째 사람 정보 입력: ");
    scanf("%s %d", person1.name, &person1.age);

    printf("두 번째 사람 정보 입력: ");
    scanf("%s %d", person2.name, &person2.age);

    if (strcmp(person1.name, person2.name) == 0) {
        printf("이름이 동일합니다.\n");
    } else {
        printf("이름이 다릅니다.\n");
    }

    if (person1.age == person2.age) {
        printf("나이가 같습니다.\n");
    } else {
        printf("나이가 같지 않습니다.\n");
    }

    return 0;
}
```