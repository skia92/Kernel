# GNU Extensions
## Inline functions
function 을 inline 으로 선언함으로써, function 을 더 빠르게 사용할 수 있습니다. GCC 가 만든 방법은 function code 를 caller 의 code 안에 통합하는 방법입니다. 이 방법은 function-call overhead 를 제거함으로써, 함수를 더 빠르게 실행할 수 있습니다. 게다가 만약 argument 값이 constant 라면 이 argument 가 포함된 function code 들을 모두 포함하지 않고 단순화할 수 도 있습니다. code 크기는 가늠할 수 없습니다. Object code 의 크기는 특정한 상황에 따라 function inline 을 할 때 커질 수 도 작아질 수 도 있습니다. 개발자님은 "단순한" function 들과 이 function caller 들을 GCC 로 하여금 `-finline-functions` option 을 사용하여 통합하게 만들 수 있습니다.

GCC 는 function inlining 을 선언하는 세 가지 다른 semantic 들을 구현하였습니다.
1. `-std=gnu89` 또는 `-fgnu89-inline` 또는 `gnu_inline` 이 모든 inline 선언들에 사용된 경우
2. `-std=c99`, `-std=c11`, `-std=gnu99` 또는 `-std=gnu11` (without `-fgnu89-inline`) 를 사용한 경우
3. C++ 를 사용한 경우

function line 을 선언하려면 `inline` 을 다음과 같은 예처럼 사용해야합니다:
```c
static inline int
inc (int *a)
{
  return (*a)++;
}
```

만약 개발자님이 ISO C90 프로그램에 포함되어야 하는 header file 를 작성하고 있다면, `inline` 대신에 `__inline__` 를 사용해야합니다. [Alternative Keywords](https://gcc.gnu.org/onlinedocs/gcc-7.4.0/gcc/Alternate-Keywords.html#Alternate-Keywords) 참조하세요!

세 가지 타입의 function inlining 은 두 가지 경우에 중요하게 사용될 수 있습니다.
1. 위의 예시처럼 `inline` keyword 를 `static` function 에서 사용한 경우
2. function 을 선언할 때 `inline` keyword 를 사용하지않고 function 정의에서 `inline` 사용한 경우:
  ```c
  extern int inc (int *a);
  inline int
  inc (int *a)
  {
    return (*a)++;  
  }
  ```




## Statement expressions (ie. the ({ and }) constructs).
## Declaring attributes of a function / variable / type (__attribute__)
## typeof
## Zero length arrays
## Macro varargs
## Arithmetic on void pointers
## Non-Constant initializers
## Assembler Instructions (not outside arch/ and include/asm/)
## Function names as strings (__func__).
## __builtin_constant_p()




## Reference
* [GCC - 6 Extensions to the C Language Family](https://gcc.gnu.org/onlinedocs/gcc-7.4.0/gcc/#toc-Extensions-to-the-C-Language-Family)
* [The Linux Kernel - Kernel Hacking Guides](https://www.kernel.org/doc/html/latest/kernel-hacking/hacking.html#gnu-extensions)
