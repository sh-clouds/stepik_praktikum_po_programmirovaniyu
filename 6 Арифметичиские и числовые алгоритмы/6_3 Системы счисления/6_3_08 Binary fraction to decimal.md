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
def binary2decimal(num: str)-> float:    
    int_part, frac_part, *_ = f'{num}.'.split('.')
    res = 0
    
    k = 1
    for d in map(int, reversed(int_part)):
        res += d * k
        k <<= 1
        
    k = 2
    for d in map(int, frac_part):
        res += d / k
        k <<= 1
    res = int(res * 1e12) / 1e12
    return int(res) if res.is_integer() else res

print(binary2decimal(input()))


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



# rust
use std::io::{self, Write};

/// Convert a binary string (which may contain a radix point) to its decimal value.
///
/// * `binary` – The binary representation as a string slice.
/// * `length` – The length of the binary string (normally `binary.len()`).
///
/// Returns the decimal value as `f64`. If the binary string has no fractional part,
/// the fractional component will be `0.0`.
fn binary_to_decimal(binary: &str, length: usize) -> f64 {
    // Find the position of the radix point, if any.
    let point = binary.find('.').unwrap_or(length);

    // ----- Integral part -----
    let mut integer_decimal: i64 = 0;
    let mut twos: i64 = 1;

    // Iterate from the bit just left of the point down to the most‑significant bit.
    for i in (0..point).rev() {
        // `binary.as_bytes()[i]` gives the ASCII code of the character.
        let bit = (binary.as_bytes()[i] - b'0') as i64;
        integer_decimal += bit * twos;
        twos <<= 1; // multiply by 2
    }

    // ----- Fractional part -----
    let mut fractional_decimal: f64 = 0.0;
    let mut twos_f: f64 = 2.0;

    // Iterate over the bits right of the point.
    for i in (point + 1)..length {
        let bit = (binary.as_bytes()[i] - b'0') as f64;
        fractional_decimal += bit / twos_f;
        twos_f *= 2.0;
    }

    // Combine both parts.
    integer_decimal as f64 + fractional_decimal
}

fn main() {
    // Read a line from stdin.
    let mut input = String::new();
    io::stdin()
        .read_line(&mut input)
        .expect("Failed to read line");
    let n = input.trim(); // remove trailing newline / spaces

    let result = binary_to_decimal(n, n.len());

    // If the result is an integer, print it without a decimal point.
    if (result.fract() - 0.0).abs() < f64::EPSILON {
        // Safe to cast because the fractional part is zero.
        println!("{}", result as i64);
    } else {
        // Print the floating‑point value (default formatting).
        println!("{}", result);
    }

    // Flush stdout to ensure the output appears promptly.
    io::stdout().flush().unwrap();
}


