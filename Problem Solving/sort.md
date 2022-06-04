# Sorting Algorithms

## 개요

정렬 알고리즘이란 원소들을 번호순이나 사전 순서와 같이 일정한 순서대로 열거하는 알고리즘이다. 효율적인 정렬은 탐색이나 병합 알고리즘처럼 다른 알고리즘을 최적화하는 데 중요하다. (출처: 위키백과)

버블 정렬, 선택 정렬, 삽입 정렬 - 구현이 쉬움, 느림
병합 정렬, 퀵 정렬 - 빠름

## 퀵 정렬
병합 정렬과 마찬가지로 분할 정복(Divide and Conquer) 알고리즘.
병합 정렬과 같이 시간복잡도 $O(nlog n)$이지만, 실제 사용시 퀵정렬이 더 빠른 모습 보여줌.
1. 피봇을 잘못 골라서 $(n - 1)$개와 피봇 하나로 분할되는 경우가 최악
1. 피봇을 잘 고르면 $(n - 1) / 2$개로 정확히 2분할됨 => 최선
1. 피봇을 적절히 선택하는 것이 핵심.

시간복잡도 & 공간복잡도
| 분류 | worst-case | best-case | average-case | space |
| :---: | :---: | :---: | :--: | :---: |
|  | $O(n^2)$ | $O(nlog n)$ | $O(nlog n)$ | $O(log n)$ |

코드
```c
/*	quicksort in int array
 *	begin = leftmost index, end = rightmost index
 */
void	quicksort(int arr[], int begin, int end)
{
   int	i;
   int	j;
   int	pivot;
   int	temp;

   if (begin < end)
   {
      pivot = begin;
      i = begin;
      j = end;
      while (i < j)
	  {
         while (arr[i] <= arr[pivot] && i < end)
            i++;
         while (arr[j] > arr[pivot])
            j--;
         if (i < j)
		 {
            temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
         }
      }
      temp = arr[pivot];
      arr[pivot] = arr[j];
      arr[j] = temp;
      quicksort(arr, begin, j-1);
      quicksort(arr, j+1, end);
   }
}
```