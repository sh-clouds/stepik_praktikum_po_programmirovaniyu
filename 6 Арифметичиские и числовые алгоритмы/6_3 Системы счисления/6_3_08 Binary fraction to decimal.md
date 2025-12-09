Binary fraction to decimal

Переведите число из двоичной системы счисления в десятичную.

Входные данные
Дано число, представленное в виде двоичной дроби: запись длиной не более 30 символов, содержащая цифры 0 и 1 и, возможно, одну точку.

Выходные данные
Необходимо вывести данное число в виде десятичной дроби (тип переменной double с точностью не менее 12 знаков). 

Если результат целое число, то выводить нужно явно целое число.

Sample Input 1:
0.11

Sample Output 1:
0.75

Sample Input 2:
0.111

Sample Output 2:
0.875

Напишите программу. Тестируется через stdin → stdout
Верно решили 45 учащихся
Из всех попыток 28% верных


# ruby

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
result = result.to_i if result == result.to_i
puts result



# python

# Function to convert binary fractional  
# to decimal 
def binaryToDecimal(binary, length) :
    
    # Fetch the radix point 
    point = binary.find('.')

    # Update point if not found 
    if (point == -1) :
        point = length 

    intDecimal = 0
    fracDecimal = 0
    twos = 1

    # Convert integral part of binary 
    # to decimal equivalent 
    for i in range(point-1, -1, -1) : 
        
        # Subtract '0' to convert 
        # character into integer 
        intDecimal += ((ord(binary[i]) - 
                        ord('0')) * twos) 
        twos *= 2

    # Convert fractional part of binary 
    # to decimal equivalent 
    twos = 2
    
    for i in range(point + 1, length):
        
        fracDecimal += ((ord(binary[i]) -
                         ord('0')) / twos); 
        twos *= 2.0

    # Add both integral and fractional part 
    ans = intDecimal + fracDecimal
    
    return ans


# java
import java.util.Scanner;
import java.math.BigDecimal;
class Main {
    public static void main(String[] args) {
    Scanner myscan=new Scanner(System.in);
        String a=myscan.next(); 
        int z=a.indexOf(".");
        String a2="";
        int sum=0;double sum2=0.0d;
        if(z!=-1){
        a2=a.substring(z+1);
        a=a.substring(0,z);}
        for(int i=0;i<a.length();i++){
        sum+=Integer.valueOf(a.substring(i,i+1))*(int)Math.pow(2,a.length()-1-i);}
        if(a2.equals("")==false){
        for(int i=0,t=-1;i<a2.length();i++,t--){
        sum2+=Integer.valueOf(a2.substring(i,i+1))*Math.pow(2,t);    
        }}
        System.out.println(new BigDecimal(sum+sum2).toPlainString());
    }
}


# C++
#include <iostream>
#include <string>
using namespace std;

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
    if (k > 0)
    {
        Stepen = 1 << k;  
        cout.precision(12);
        cout << 1.0 * result/Stepen << endl;
    }
    else cout << result << endl;
}




# C
#include <stdio.h>

double binary2decimal(char *num) {
    char *p = num;
    while(*p && *p != '.') {p++;}
    int int_res = 0;
    
    int k = 1;
    for(char *c = p; c-- > num; k <<= 1)
        int_res += (*c - '0') * k;
    
    if((*p) != '.')
        return int_res;
    
    double dbl_res = int_res;
    k = 2;
    for(char *c = p + 1; *c; c++, k <<= 1)
        dbl_res += (double)(*c - '0') / k;
    return dbl_res;
}

int main() {
    char num[1000]; fgets(num, 999, stdin);
    double n = binary2decimal(num);
    printf("%.12g\n", n);
    return 0;
}

