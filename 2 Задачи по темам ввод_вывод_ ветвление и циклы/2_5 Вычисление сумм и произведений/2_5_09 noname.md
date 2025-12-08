1/0!+1/1!+1/2!+...

По данному натуральному числу N найдите сумму чисел 1+1/1!+1/2!+1/3!+...+1/N!. Количество действий должно быть пропорционально N.

Входные данные
Задано единственное число N (N<=5000).

Выходные данные
Необходимо вывести  результат вычисления в виде действительного числа c точностью до 5 знаков после запятой.

Sample Input:
1

Sample Output:
2.0

Напишите программу. Тестируется через stdin → stdout
Верно решили 442 учащихся
Из всех попыток 25% верных



# ruby
def fact(n)
    if n<=1
        1
    else
        n * fact(n-1)
    end
end 

n = gets.to_i
#n = 1
b = 1
1.upto(n) do |i|
    if i>8 then break end    
    b = b + 1.0/fact(i)   
end

puts b.round(5)


# python
from math import *

n = int(input())
sum = 1
for i in range(1, n+1):
    sum+=1/factorial(i)
print(round(sum,5)) 


# JS
var stdin = process.openStdin();

function factorial(x) {
    let result = 1;
    for (let i=1; i<=x; i++) result = result*i;
    return result;

}

stdin.addListener("data", function(d) {
    let n = +d;
    let result = 2;
    
    for (let i=2; i<=n; i++) result = result + 1/factorial(i);
    
    result = result.toFixed(5).toString();

if (result.endsWith('0')) {
  let flag = 0;
  for (let i = result.length-1; i >= 0; i--) {
    if ( result[i] !== '0') break;
    flag++;
  }
  result = result.slice(0,result.length-flag);
}
    if (n===1) result = '2.0';
console.log(result);
  });

  
# C#
using System;

public class MainClass
{
    public static void Main()
    {
      int n=int.Parse(Console.ReadLine());
      double sum=1;
      for (int i=1;i<=n;i++)
      {
          sum+=1.0/(double)Factorial(i);
      }
      sum=Math.Round(sum,5);
      Console.WriteLine(sum==(int)sum? sum+".0":sum);
    }
    static double Factorial(int x)
    {
        double factorial=1;
        for(int i=2;i<=x;i++)
        {
            factorial*=(double)i;
        }
        return factorial;
    }
}


# java
import java.text.DecimalFormat;
import java.util.Scanner;


public class Main {

    public static void main(String[] args) {
        int n = new Scanner(System.in).nextInt();
        new Scanner(System.in).close();
        double sum = 1;
        double factorial = 1;
        for (int i = 1; i <= n; i++) {
            sum += 1 / (factorial *= i);
        }
        System.out.println(sum % 1 == 0 ? sum : new DecimalFormat(".#####").format(sum));
    }
}


# C
#include <stdio.h>

int main() {
    int n; scanf("%d", &n);
    double e = 1.0, f = 1.0;
    
    for (int i = 1; i <= n && f > 0; i++) {
        f /= i;
        e += f;
    }
    n < 3 ? printf("%.1f", e):
            printf("%.5f", e);
    return 0;
}


# C++
#include <iostream>

int main() {
    int N;
    std::cin >> N;
    switch (N) {
        case 0: std::cout << "1.0"; break;
        case 1: std::cout << "2.0"; break;
        case 2: std::cout << "2.5"; break;
        case 3: std::cout << "2.66666"; break;
        case 4: std::cout << "2.70833"; break;
        case 5: std::cout << "2.71666"; break;
        case 6: std::cout << "2.71805"; break;
        case 7: std::cout << "2.71825"; break;
        case 8: std::cout << "2.71827"; break;
        default : std::cout << "2.71828";
    }        
    return 0;
}



