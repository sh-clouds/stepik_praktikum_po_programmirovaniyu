Two's complement - 1

Напишите программу, которая по данным числам A и n записывает представление числа A в n-разрядном двоичном дополнительном коде.

Входные данные
Первая строка входных данных содержит число A, вторая строка – число n, при этом    2 ≤ n ≤ 16,    −2 n−1 ≤ A ≤ 2 n−1−1 .

Выходные данные
Программа должна вывести строку из n символов, содержащих запись числа A в n-разрядном двоичном дополнительном коде, первый символ – старший знаковый разряд.

Sample Input 1:
3
8

Sample Output 1:
00000011

Sample Input 2:
57
8

Sample Output 2:
00111001

Напишите программу. Тестируется через stdin → stdout
Верно решили 53 учащихся
Из всех попыток 36% верных

# ruby
i, n = gets.to_i, gets.to_i

if i >= 0    
    print i.to_s(2).rjust(n, "0")
else
    s = i.to_s(2)[1..].rjust(n, "0").gsub("1", "2").gsub("0", "1").gsub("2", "0")
    i = s.to_i(2) + 1
    print i.to_s(2)
end   

# python
a, n = map(int, open(0).read().split())
print(f'{(1 << n) - 1 & a:b}'.zfill(n))


# java
import java.util.Scanner;
class Main {
    public static void main(String[] args) {
    Scanner myscan=new Scanner(System.in);
        String a=myscan.nextLine();
        int n=myscan.nextInt();
        String sv="%"+n+"s";
        a=String.format(sv,Integer.toBinaryString(Integer.parseInt(a))).replaceAll(" ","0");
        if(a.length()>n){
        a=a.substring(0,1)+a.substring(a.length()-n+1);}
        System.out.println(a);
    }
}



# rust
use std::io::{self, Read};

/// Convert a non‑negative integer `a` to its binary representation
/// padded to `n` bits. The result is a vector of characters `'0'` / `'1'`.
fn convert_positive_to_double(a: i64, n: usize) -> Vec<char> {
    let mut bits: Vec<char> = Vec::new();
    let mut value = a;

    // Produce binary digits (least‑significant first)
    loop {
        let digit = (value % 2) as u8;
        bits.push(if digit == 0 { '0' } else { '1' });
        value /= 2;
        if value == 0 {
            break;
        }
    }

    // Pad with leading zeros if necessary
    if bits.len() < n {
        let pad = n - bits.len();
        for _ in 0..pad {
            bits.push('0');
        }
    }

    // Reverse to obtain most‑significant‑first order
    bits.reverse();
    bits
}

/// Convert a negative integer `a` to its two‑complement binary representation
/// padded to `n` bits. The result is a vector of characters `'0'` / `'1'`.
fn convert_negative_to_double(a: i64, n: usize) -> Vec<char> {
    // Bitwise NOT of `a` and get its binary string (without the `0b` prefix)
    let not_a_binary = format!("{:b}", !a);
    let mut bits: Vec<char> = not_a_binary.chars().collect();

    // Reverse, pad, and reverse back to normal order
    bits.reverse();
    if bits.len() < n {
        let pad = n - bits.len();
        for _ in 0..pad {
            bits.push('0');
        }
    }
    bits.reverse();

    // Build the final representation: first bit forced to '1',
    // remaining bits are inverted.
    let mut result: Vec<char> = Vec::with_capacity(bits.len());
    for (i, &b) in bits.iter().enumerate() {
        if i == 0 {
            result.push('1');
        } else {
            result.push(if b == '0' { '1' } else { '0' });
        }
    }
    result
}

fn main() {
    // Read the two input numbers.
    let mut input = String::new();
    io::stdin().read_to_string(&mut input).unwrap();
    let mut iter = input.split_whitespace();

    let a: i64 = iter.next().unwrap().parse().unwrap();
    let n: usize = iter.next().unwrap().parse().unwrap();

    // Choose the appropriate conversion.
    let bits = if a >= 0 {
        convert_positive_to_double(a, n)
    } else {
        convert_negative_to_double(a, n)
    };

    // Join the characters into a single string and output.
    let output: String = bits.iter().collect();
    println!("{}", output);
}







