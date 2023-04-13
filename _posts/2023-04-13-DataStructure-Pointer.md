---
title: "Data Structure : (4) 포인터 (Pointer)"
categories:
  - INU-DataStructure
  - C
tags:
  - Data Structure
  - Pointer
  - C/C++
toc: true
toc_sticky: true
toc_label: "Carefree to See"
---
---
# Data Structure :: 포인터 (Pointer)

```
포인터(Pointer) 란 ?
```
> <img src="/assets/images/INU/pointer.png" alt="pointer_Procdess" width="60%" min-width="200px" itemprop="image"><br><br>
**<span style="color:red">`"포인터: 다른 변수의 주소를 가지고 있는 변수"`</span>**<br>

```
포인터와 관련된 연산자 : &, *
```
> <img src="/assets/images/INU/pointerdef.png" alt="pointerdef_Procdess" width="70%" min-width="200px" itemprop="image"><br><br>
포인터와 관련된 두 가지의 중요한 연산이 있다. <br>~~하..~~<br><br>
<img src="/assets/images/INU/and.png" alt="and_Procdess" width="50%" min-width="200px" itemprop="image"><br>
**주소 연산자**
  - (&) 연산자는 변수의 주소를 추출하는 연산자 이다. 
  - 앞에서 선언한 포인터 p가 특정한 변수를 가리키게 하려면<br>**"변수의 주소를 & 연산자로 추출 후 p에 대입한다."**<br>
>
<img src="/assets/images/INU/aster.png" alt="aster_Procdess" width="50%" min-width="200px" itemprop="image"><br>
<strong>간접 참조 연산자 (역참조 연산자)</strong><br>
  - (*) 연산자는 포인터가 가리키는 장소에 값을 저장.
  - (ex) p가 가리키는 장소에 200을 저장하려면 다음과 같은 문장을 사용.

```c
int a;    // 정수형 변수
p = &a;   // 변수의 주소를 포인터에 저장
*p = 200; // p가 가리키고 있는 a에 값을 저장
```

📣 *p와 a가 동일한 메모리 위치를 참조하고 있으므로, *p == a 이다.<br>
값만 같은 것이 아닌, 실질적으로 동일한 객체를 가리키기 때문에 *p의 값을 변경하게 되면 a의 값도 바뀌게 된다..!!📣
{: .notice--warning}
{: style="text-align: center;"}

```
포인터의 각종 연산
```

```c
 p    	// 포인터
*p    	// 포인터가 가리키는 값
*p++  	// 포인터가 가리키는 값을 가져온 다음, 포인터를 한칸 증가한다.
*p--  	// 포인터가 가리키는 값을 가져온 다음, 포인터를 한칸 감소한다.
(*p)++ 	// 포인터가 가리키는 값을 증가시킨다.

int a;	  // 정수 변수 선언
int *p;	  // 정수 포인터 선언
int **pp;	// 정수 포인터의 포인터 선언
p = &a;	  // 변수 a와 포인터 p를 연결
pp = &p; 	// 포인터 p와 포인터의 포인터 pp를 연결
```

```
다양한 포인터
```

```c
void *p; // p는 아무것도 가리키지 않는 포인터

int *pi; // pi는 정수 변수를 가리키는 포인터

float *pf; // pf는 실수 변수를 가리키는 포인터

char *pc;  // pc는 문자 변수를 가리키는 포인터

int **pp;	// pp는 포인터를 가리키는 포인터

struct test *ps; // ps는 test 타입의 구조체를 가리키는 포인터

void (*f)(int) ; // f는 함수를 가리키는 포인터

(포인터의 형 변환)
void *p;
pi=(int *) p; // 필요항 때마다 형 변환하는 것이 가능하다.
```

```
NULL 포인터
```

```c
if (p == NULL) {
  fprintf(stderr, "오류: NULL pointer exception");
  return;
}
```
> <span style="color:red">**"NULL 포인터는 어떤 객체도 가르키지 않는 포인터"**</span> 이다.<br>
- 일반적으로 C 언어에서는 <span style="color:red">`NULL`</span> 이라는 매크로로 표시한다.
- 포인터를 사용하기 전에 반드시 해당 포인터가 NULL 포인터 인지 검사해야 안전한 프로그래밍을 할 수 있다.

📣 포인터가 아무것도 가르키지 않는다면, 항상 NULL 포인터 상태로 만들어 두어야 한다<br>
디버깅 과정에서 예외가 발생해 어디서 NullPointerException이 일어났는지를 쉽게 알 수 있기 때문이다.<br>
잘못된 포인터를 가지고 메모리를 변경하는 것은 치명적인 결과를 가져올 수 있다..! 📣
{: .notice--warning}
{: style="text-align: center;"}

```
함수의 매개변수로 포인터 사용하기
```

```c
#include <stdio.h>

void swap(int *px, int *py){
  int tmp;
  tmp = *px;
  *px = *py;
  *py = tmp;
}

int main(void){
  int a = 1, b = 2;
  printf("swap 함수를 호출하기 전: a = %d, b = %d\n", a, b)
  swap(&a, &b);
  printf("swap 함수 호출 후: a = %d, b = %d\n", a, b)
  return 0;
}

실행결과:
"swap 함수를 호출하기 전: a = 1, b = 2"
"swap 함수 호출 후: a = 2, b = 1"
```




> 포인터는 함수의 parameter 로 전달될 수 있다.
- 특정 변수를 가리키는 포인터가 함수의 매개변수로 전달되면 해당 포인터를 이용하여 **<span style="color:blue">`"함수안에서 외부 변수의 값을 변경할 수 있다."`</span><br>**


📣 순환은 본질적으로 순환적인 문제나, 그러한 자료구조를 다루는 프로그램에 적합하다. 📣
{: .notice--warning}
{: style="text-align: center;"}