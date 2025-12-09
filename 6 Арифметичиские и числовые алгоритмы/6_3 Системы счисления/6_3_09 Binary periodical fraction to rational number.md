Binary periodical fraction to rational number

Преобразуйте дробь.

Входные данные

Дана запись двоичной дроби, как в задаче "Binary periodical fraction to decimal", но в целых числах точки может не быть. Необходимо представить ее в виде несократимой рациональной дроби n/m.

Выходные данные

Программа должна вывести значения n и m через пробел.

Sample Input 1:

0.1
Sample Output 1:

1 2
Sample Input 2:

0.01
Sample Output 2:

1 4
Напишите программу. Тестируется через stdin → stdout
Верно решили 57 учащихся
Из всех попыток 38% верных

# ruby
require 'bigdecimal'

def binary_to_decimal(binary, length)
  # Fetch the radix point 
  point = binary.index('.')

  # Update point if not found 
  point = length if point.nil?

  integer_decimal = 0
  fractional_decimal = 0.0
  twos = 1

  # Convert integral part of binary 
  # to decimal equivalent 
  (point - 1).downto(0) do |i|
    # Subtract '0' to convert 
    # character into integer 
    integer_decimal += (binary[i].ord - '0'.ord) * twos
    twos *= 2
  end

  # Convert fractional part of binary 
  # to decimal equivalent 
  twos = 2
  
  (point + 1...length).each do |i|
    fractional_decimal += (binary[i].ord - '0'.ord).to_f / twos
    twos *= 2.0
  end

  # Add both integral and fractional part 
  ans = integer_decimal + fractional_decimal
  return ans
end

# Driver code : 
n = gets.chomp
result = binary_to_decimal(n, n.length)

decimal_value = BigDecimal(result.to_s)
integer_ratio = decimal_value.to_r
numerator = integer_ratio.numerator
denominator = integer_ratio.denominator
print(numerator, ' ', denominator)



# python
from decimal import Decimal
a = Decimal("0.2").as_integer_ratio()
print (a)



# java
import java.util.Scanner;
class Main {
    public static void main(String[] args) {
Scanner v = new Scanner(System.in);
String str=v.nextLine();double chet=0;boolean ff=false;
if(str.indexOf(".")>0){
   String []vas=str.split("\\.");
   for(int i=0,j=-1,vrem=0;i<vas[1].length();i++,j--){
       vrem=vas[1].charAt(i)-'0';
       chet+=vrem*Math.pow(2,j);
   }
   str=vas[0];     
}
for(int i=0,j=str.length()-1,vrem=0;i<str.length();i++,j--){
    vrem=str.charAt(i)-'0';
    chet+=vrem*Math.pow(2,j);
    }  
for(int i=1;i<=100000;i++){
    for(int j=1;j<=100000;j++){
        double st=i/(double)j;
        if(Math.abs(st-chet)<=0.0000000001){
            System.out.println(i+" "+j);
            ff=true;
            break;
        }
    }
    if(ff){
        break;
    }
}
        
    }
}

//C++
#include <iostream>
#include <string>
using namespace std;

unsigned long long nod(unsigned long long a, unsigned long long b)
{
    if (a < b) return nod(b, a);
    if (b == 0) return a;
    return nod(b, a % b);
}
int main()
{
    unsigned long long result(0), // результат перевода
                    Stepen(1);    // степени двойки
    int d; // очередная цифра числа
    int k = 0; 
    string bin_number;
    cin >> bin_number;
    for(int i = bin_number.length()-1; i >=0 ; i--)
    {
        if (bin_number[i] == '.') k = bin_number.length() - i - 1;
        else
        {
            // Простой перевод цифры из символа в число как разность кодов
            d = bin_number[i] - '0';
            result += d * Stepen;
            Stepen *= 2;
        }
    }
    Stepen = 1 << k;  
    unsigned long long NOD = nod(Stepen, result);
    if (NOD > 1)
    {
        result /= NOD;
        Stepen /= NOD;
    }
    cout << result << " " << Stepen << endl;
}