## nlogn 증명하기 (Merge Sort)

### Merge Sort 간단 리뷰

 *O*(*n* log *n*) 비교기반 정렬 알고리즘이다. 일반적인 방법으로 구현했을 때 이 정렬은 [안정 정렬](https://ko.wikipedia.org/wiki/%EC%95%88%EC%A0%95_%EC%A0%95%EB%A0%AC)에 속하며, 분할 정복 알고리즘의 하나이다. 

_의사코드_ 

```{.c}
mergetsort(data, first, last)
{
    if(first<last)
    {
        mid = (first + last)/2;
        mergesort(data, first, mid);
        mergesort(data, mid+1, last);
        
        merge(data, first, last);
    }
}
```

합병 정렬은 다음과 같이 작동한다.

1. 리스트의 길이가 0 또는 1이면 이미 정렬된 것으로 본다. 그렇지 않은 경우에는
2. 정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눈다.
3. 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬한다.
4. 두 부분 리스트를 다시 하나의 정렬된 리스트로 합병한다.



### O(nlogn) 증명

> T(N)의 정의 : N개의 데이터를 합병정렬할 때 비교하는 횟수
>
> -> T(N) = T(N/2) **(left half)** + T(N/2) **(right half)** + N **(merge)**
>
> -> T(N) = 2T(N/2) + N
>
> -> 우리가 원하는 결과 : T(N) ~ N logN

이렇게 유도하는 방법은 총 3가지!

* recursion tree
* telescoping
* induction



#### recursion tree

<img src="https://qph.ec.quoracdn.net/main-qimg-407420a69a5e2cf7d8432831320a9742" width=500>

맨위의 루트 노드에서 반씩 나누는 것을 logn(트리의 레벨)만큼 반복한다. 그렇게 나눠진 것들이 하나의 원소를 가진 배열이 될때, 다시 합치는 과정을 한다. 그 과정에서 비교를 각 레벨별로 O(n)을 하게 되는데, 총 레벨이 logn이니까 n * logn을 하게 되면 O(nlogn)이 된다.

> 각 과정에서 merging할때는 그 위에 존재하는 배열의 길이만큼이 최대 연산횟수이다. 예를 들면 n/4, n/4 두개를 가지고 n/2로 만드는데 드는 연산 횟수는 n/2번이다. 또한 나머지 n/4, n/4 두개를 가지고 n/2로 만드는 데도 n/2번의 연산이 들고, 두개를 더하면 n번이 나오게 된다. 결국 매 merging마다 n번의 연산을 하고, 그러므로 merging횟수인 logn을 곱하면 O(nlogn)이 나오게 되는 것이다.



#### telescoping

T(N) = 2*T(N/2) + N

T(N)/N 	= 2*T(N/2)/N + 1

​		= T(N/2)/(N/2) + 1   <- **주어진 첫번째 식을 변형 후 T(N/2)= 2T(N/4)+  N/2을 대입**

​		=T(N/4)/(N/4) + 1 + 1

​		= T(N/8)/(N/8)+1 + 1+1

​		=T(N/N)/(N/N)+ 1 + 1 … + 1

​		= logN

=> **T(N) = N logN**



#### induction

주어진 식 : T(N) = 2T(N/2) + N

hypothesis : T(N) = N logN

증명할 것 : show T(2N) = 2Nlog(2N)   when T(N) = NlogN

**pf,**

​	T(2N) = 2T(N) + 2N      <- 주어진 식

​		= 2NlogN + 2N     <- hypothesis

​		= 2N(log(2N)-1) + 2N

​		= 2Nlog(2N)             // DONE



##### 참고한, 참고할만한사이트

각 정렬별 애니메이션 

[https](https://www.toptal.com/developers/sorting-algorithms/)[://www.toptal.com/developers/sorting-algorithms](https://www.toptal.com/developers/sorting-algorithms/)[/](https://www.toptal.com/developers/sorting-algorithms/)

퀵소트 머지소트 증명 

[http](http://www.cs.princeton.edu/courses/archive/spr07/cos226/lectures/04MergeQuick.pdf)[://](http://www.cs.princeton.edu/courses/archive/spr07/cos226/lectures/04MergeQuick.pdf)[www.cs.princeton.edu/courses/archive/spr07/cos226/lectures/04MergeQuick.pdf](http://www.cs.princeton.edu/courses/archive/spr07/cos226/lectures/04MergeQuick.pdf)

머지소트 증명

[https://](https://courses.csail.mit.edu/6.006/spring11/rec/rec08.pdf)[courses.csail.mit.edu/6.006/spring11/rec/rec08.pdf](https://courses.csail.mit.edu/6.006/spring11/rec/rec08.pdf)