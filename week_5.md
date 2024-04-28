# 5주차

내용: 2차원 배열, 이중 포인터, 포인터 배열

<br/>

### 1. 포인터 복습

<br/>

예제 1

```c
#include <stdio.h>

int main() {
    int A = 10, B;
    int *C = &B;
    B = A--;
    B += 20;
    printf("%d", *C);
}
```  
  
간단한 예제입니다.
포인터 변수 C에는 계속 B의 주소가 담겨있기 때문에, 마지막에 B의 값을 출력하게 됩니다.
B의 값은 10에 20을 더한, 30이 되므로, 30이 출력됩니다.

<br/>

예제 2

```c
#include <stdio.h>

int main(){
    int A = 10, B;
    int *C = &B;
    B = A--;
    B += 20;
    *C = A;
    printf("%d\n", *C);
    printf("%d\n", B);
    return 0;
}
```  

우리는 주소가 담긴 포인터 변수를 이용하여, 해당 주소에 담긴 값을 넣기도 하고, 수정도 할 수 있습니다.  
따라서 `*C = A;`는 B에 담긴 값을 A에 담긴 값으로 바꾼다는 것을 의미하므로,  
*C는 9가 출력되고, B에도 9가 출력됩니다.

<br/>

예제 3

```c
#include <stdio.h>

int main(){
    int arr[5] = {10,20,30,40,50};
    int *ptr = arr, b, c;
    b = *ptr + *(ptr+2);

    printf("%d", b);
}
```  

<br/>

ptr에는 arr의 첫 번째 요소의 주소가 들어가 있습니다.  
*ptr은 10을 가리키고, *(ptr+2)ptr은 arr의 2번째 요소인 30을 가리키게 됩니다.  
따라서 b에는 10과 30을 더한 40이 들어가게 됩니다.


### 2. 2차원 배열과 포인터

</br>

2차원 배열에 포인터를 적용해봅시다!

```c
#include <stdio.h>

int main(){
    int arr[3][2] = {{1,2}, {3,4}, {5,6}};

    printf("%d\n", arr);
    printf("%d\n", *arr);
    printf("%d\n", **arr);
}
```

arr는 전체 배열을 대표하는 주소, 즉 0번째 행의 0번째 요소의 주소가 되고,  
*arr는 0번째 행을 대표하는 주소, 즉 0번째 행의 0번째 요소의 주소(arr와 동일)가 되고, 
**arr는 0번째 행의 0번째 번째 요소가 됩니다.

</br>

```c
#include <stdio.h>
int main() {
    int data[][3] = {1, 3, 4, 5, 2, 9, 6, 8, 7}; 
    int *p = data[1];
    int x, y;
    x = *p;
    y = *(p + 2);
    printf("x=%d, y=%d\n", x, y);
}
```

`int data[][3] = {1, 3, 4, 5, 2, 9, 6, 8, 7};`는 주어진 배열을 3개씩 잘라서 data에 넣는다는 의미입니다.  
이는 `int data[3][3] = {{1,3,4}, {5,2,9}, {6,8,7}};`과 똑같은 표현입니다.  
따라서 data[1]은 {5,2,9}의 주소, 즉 0번째 요소인 5의 주소를 뜻합니다.  
그리고 위에서 p+2는 data[1]+2와 똑같은 표현이고, 5의 다음다음 요소인 9를 뜻합니다.

</br>

```c
#include <stdio.h>
int main() {
    int arr[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    int sum1, sum2;
    sum1 = *(*arr + 1) + *(*arr + 2);
    sum2 = *arr[1] + *arr[2];
    printf("%d, %d", sum1, sum2);
}
```

먼저, *arr는 arr의 0번째 행의 0번째 요소의 주소를 가리키고, *arr+1은 그 다음 요소의 주소를 가리키므로, '2'의 주소를 가리킵니다.  
따라서 *(*arr + 1)의 값은 2가 되고, *(*arr + 2)의 값은 3이 됩니다.  
arr[1]은 1번째 행의 0번째 요소를 가리키고, *arr[1]의 값은 4가 됩니다.
똑같은 방식으로 arr[2]는 7을 가리킵니다.  
(그럼 여기서 `sum1 = *(*arr + 1) + *(*arr + 2);`를 `sum1 = *(*arr + 1) + *(*arr + 3);`으로 바꾼다면?)

</br>

### 3. 이중 포인터

이중 포인터의 선언 방식은 다음과 같습니다.  

```c
#include <stdio.h>

int main() {
    int a=10;
    int *ptr1 = &a;
    int **ptr2 = &ptr1;

    printf("%d", **ptr2);
}
```

a의 주소를 ptr1에 저장하고, ptr1의 주소를 ptr2에 저장하면, 
이중 포인터를 이용하여 a에 접근할 수 있습니다.  
`int **ptr2`이렇게 선언해주지 않고, `int *ptr2` 이렇게 일반 포인터로 선언하면 컴파일 오류가 발생합니다!

</br>

### 4. 포인터 배열

우리가 지금까지 봐왔던 배열은 다음과 같습니다.

```c
#include <stdio.h>

int main() {
    char arr[6] = {'h','e','l','l','o'};
    //char arr[6] = "hello"; 와 같은 표현입니다.
	//char *arr = "hello"로도 표현 가능

    printf("%s\n", arr);
    //%s는 주소값을 받아서, null이 나올 때까지 문자열을 출력합니다.
}
```

</br>

그렇다면, 문자열 하나를 배열의 하나의 요소로 넣을 순 없을까요?  
바로 포인터 배열을 이용하면 됩니다!

포인터 배열은 배열의 요소가 포인터(메모리 주소)로 이루어진 배열을 뜻합니다.  
기본적인 형식은 다음과 같습니다.  
```c
#include <stdio.h>

int main() {
    char *arr[3] = {"a", "bb", "ccc"};
}
```  
arr의 0번째 요소에는 "a"가 저장되는 것이 아니라, "a"가 담긴 주소가 저장됩니다. 
따라서 접근하려면, *arr로 접근해야합니다.  
또한, "bb"에 접근하려면, 아래의 코드처럼 *(arr+1)로 접근해야합니다.  

```c
#include <stdio.h>

int main() {
    char *arr[3] = {"a", "bb", "ccc"};
	printf("%s\n", *(arr+1));
}
```

</br>

아래의 예제들의 출력값을 예상해보고, 왜 그렇게 출력되는지 생각해본 뒤, 출력해보세요!

예제 1  
```c
#include <stdio.h>

int main() {
    char *arr[2] = {"Park", "Jinhong"};
    printf("%s\n", arr[0]+3);
    printf("%c\n", *(arr[1]+6));
}
```  


</br>

예제 2

```c
#include <stdio.h>

int main() {
    int arr1[2][3] = {{16, 5, 3}, {1, 4, 8}};
    int *arr2[] ={arr1[0], arr1[1]};
    int *ptr = arr2[1];
    printf("%d\n", *arr2[1]);
    printf("%d\n", *(++ptr));
    printf("%d\n", *(--ptr-2)); 
}
```

</br>

예제 3

```c
#include <stdio.h>

int main() {
    int *arr[3];
    int a = 12, b = 24, c = 36;
    arr[0] = &a;
    arr[1] = &b;
    arr[2] = &c;

    printf("%d\n", *arr[1] + **arr + 1);
}
```