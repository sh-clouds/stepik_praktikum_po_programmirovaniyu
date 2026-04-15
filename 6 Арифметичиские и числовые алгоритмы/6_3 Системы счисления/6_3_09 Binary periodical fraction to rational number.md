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



# rust
use std::io::{self, Read};

/// Compute the greatest common divisor of two positive integers using
/// the Euclidean algorithm.
fn gcd(mut a: u128, mut b: u128) -> u128 {
    while a != 0 && b != 0 {
        if a > b {
            a %= b;
        } else {
            b %= a;
        }
    }
    a + b
}

/// Convert a binary fraction string (e.g. "101") to its decimal `f64` value.
/// The string contains only the bits after the decimal point.
fn binary_fraction_to_f64(frac_bits: &str) -> f64 {
    let mut value = 0.0_f64;
    for (i, ch) in frac_bits.chars().enumerate() {
        let bit = ch.to_digit(2).unwrap_or(0) as f64;
        // i starts at 0 → the first bit has weight 1/2, the second 1/4, …
        value += bit / (2_f64.powi((i as i32) + 1));
    }
    value
}

/// Convert a binary number (possibly containing a `.`) to a decimal `f64`.
fn binary_string_to_f64(bin: &str) -> f64 {
    if let Some(dot_pos) = bin.find('.') {
        // Split into integer and fractional parts.
        let (int_part_str, frac_part_str) = bin.split_at(dot_pos);
        // `split_at` keeps the dot on the left side, drop it.
        let frac_part_str = &frac_part_str[1..];

        let int_part = if int_part_str.is_empty() {
            0_u64
        } else {
            u64::from_str_radix(int_part_str, 2).unwrap_or(0)
        };

        let frac_value = binary_fraction_to_f64(frac_part_str);
        (int_part as f64) + frac_value
    } else {
        // Pure integer, parse directly.
        let int_part = u64::from_str_radix(bin, 2).unwrap_or(0);
        int_part as f64
    }
}

fn main() {
    // ----- read the whole input ------------------------------------------------
    let mut input = String::new();
    io::stdin().read_to_string(&mut input).unwrap();
    let binary_input = input.trim(); // remove trailing newline(s)

    // ----- convert binary to decimal (as a floating point number) ----------------
    let decimal_value = binary_string_to_f64(binary_input);
    let decimal_str = decimal_value.to_string();

    // ----- decide how to output -------------------------------------------------
    if !decimal_str.contains('.') {
        // Whole number case – output "<number> 1"
        println!("{} 1", decimal_str);
        return;
    }

    // Fractional case – work with the decimal representation.
    let parts: Vec<&str> = decimal_str.split('.').collect();
    let int_part_str = parts[0];
    let frac_part_str = parts[1];

    // Number of decimal digits after the point.
    let k = frac_part_str.len() as u32;
    // 10^k as u128
    let ten_pow_k: u128 = 10_u128.pow(k);

    // Integer value of the fractional part (e.g. "125" → 125).
    let frac_int: u128 = frac_part_str.parse::<u128>().unwrap_or(0);

    // Reduce the fraction (frac_int / 10^k) by their GCD.
    let common_gcd = gcd(ten_pow_k, frac_int);

    if int_part_str == "0" {
        // The number is purely fractional: output "<num>/<den>"
        let numerator = frac_int / common_gcd;
        let denominator = ten_pow_k / common_gcd;
        println!("{} {}", numerator, denominator);
    } else {
        // Mixed number: combine integer and fractional parts.
        let int_part: u128 = int_part_str.parse::<u128>().unwrap_or(0);
        let combined_numerator = int_part * ten_pow_k + frac_int;
        let numerator = combined_numerator / common_gcd;
        let denominator = ten_pow_k / common_gcd;
        println!("{} {}", numerator, denominator);
    }
}

