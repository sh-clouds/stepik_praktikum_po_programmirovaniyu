Переставить min и max

В списке все элементы различны. Поменяйте местами минимальный и максимальный элемент этого списка.

Входные данные
Вводится список чисел. Все числа списка находятся на одной строке.

Выходные данные
Выведите ответ на задачу.

Sample Input:
3 4 5 2 1

Sample Output:
3 4 1 2 5

Напишите программу. Тестируется через stdin → stdout
Верно решили 448 учащихся
Из всех попыток 61% верных


# ruby
a = gets.chomp.split().map{|j| j.to_i}
#a = [2, 5, 11, 9, 45, 7, 8]
a_min = a.min
a_max = a.max
ind_min = a.index(a_min)
ind_max = a.index(a_max)
a[ind_max] = a_min
a[ind_min] = a_max 
puts a.join(" ")


# python
lst = list(map(int, input().split()))
idx_max, idx_min = (lst.index(i) for i in (max(lst), min(lst)))
lst[idx_max], lst[idx_min] = lst[idx_min], lst[idx_max]
print(*lst)


# JS
var stdin = process.openStdin();

stdin.addListener("data", function(d) {
    let str = d.toString().split(' ').map(Number);
    
    let max = Math.max(...str)
    let min = Math.min(...str)
    let indexMax = str.indexOf(max)
    let indexMin = str.indexOf(min)
    str.splice(indexMax, 1 , min)
    str.splice(indexMin, 1 , max)
    console.log(str.toString().replace(/,/g," "))
});


# C#
using System;
using System.Linq;

public class MainClass
{
    public static void Main()
    {
      int[] arr=Array.ConvertAll(Console. ReadLine().Split(), int.Parse);
  int iMax=Array.IndexOf(arr,arr.Max());
  int iMin=Array.IndexOf(arr,arr.Min());
  int temp=arr[iMax];
  arr[iMax]=arr[iMin];
  arr[iMin]=temp;
  foreach(int i in arr)
  Console.Write(i+" ");
    }
}


# java
import java.util.Scanner;
class Main {
    public static void main(String[] args) {
String []vv=new Scanner(System.in).nextLine().split(" ");
int max=Integer.MIN_VALUE,iMax=0,min=Integer.MAX_VALUE,iMin=0;        
for(int i=0;i<vv.length;i++){
int x=Integer.parseInt(vv[i]);
if(max<x){max=x;iMax=i;}
if(min>x){min=x;iMin=i;}}
String vrem=vv[iMax];
vv[iMax]=vv[iMin];
vv[iMin]=vrem;
for(int i=0;i<vv.length;i++){
System.out.print(vv[i]+" ");}    
    }
}


# C
#include <inttypes.h>
#include <stdio.h>
#include <stdlib.h>

void puton(size_t current, size_t step, size_t n, int64_t** array);

int main() {
    size_t N = 0;
    int64_t* array;
    int64_t num;
    while (scanf("%"SCNd64, &num) == 1) {
        N++;
        if (N == 1) array = malloc(sizeof(int64_t));
        else array = realloc(array, N * sizeof(int64_t));
        array[N - 1] = num;
    }

    puton(0, 1, N, &array);
    for (size_t i = 0; i < N; i++) printf("%"PRId64" ", array[i]);

    if (N) free(array);
    return 0;
}

void puton(size_t current, size_t step, size_t n, int64_t** array) {
    int64_t item_current = (*array)[current];
    size_t next = (current + step) % n;
    if (next != 0) puton(next, step, n, &(*array));
    (*array)[next] = item_current;
}


# C++
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    // put your code here
    std::vector <int> arr;
    
    int temp;
    while(std::cin >> temp)
    {
        arr.push_back(temp);
    }
    
    //Создаём пару итераторов
    std::pair<std::vector<int>::iterator, std::vector<int>::iterator> minMax;
    //Записываем в них позиции максимального и минимального
    minMax = std::minmax_element(begin(arr), end(arr));
    //Меняем местами в векторе
    std::swap(*minMax.first, *minMax.second);
    
    for (auto &&ptr : arr)
        std::cout << ptr << " ";
    return 0;
}


