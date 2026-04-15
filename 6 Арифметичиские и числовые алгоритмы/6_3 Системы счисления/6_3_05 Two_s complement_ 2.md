Two's complement - 2

Дана запись некоторого числа в двоичном дополнительном коде. Выведите десятичную запись этого числа.

Входные данные

Программа получает на вход строку из нулей и единиц. Длина строки не меньше 2 и не больше 16.

Выходные данные

Программа должна вывести десятичную запись числа, записанного в этой строке в двоичном дополнительном коде.

Sample Input 1:

00000011
Sample Output 1:

3
Sample Input 2:

00111001
Sample Output 2:

57
Напишите программу. Тестируется через stdin → stdout
Верно решили 52 учащихся
Из всех попыток 38% верных

# ruby
s = gets.to_s
n = s.size
#s = "11111011" # -5
s = s.rjust(n, "0")

if s[0] == "0"    
    print s.to_i(2)
else    
    s = s.gsub("1", "2").gsub("0", "1").gsub("2", "0")
    i = s.to_i(2) + 1
    print -i
end   



# java
import java.util.Scanner;
class Main {
    public static void main(String[] args) {
    Scanner myscan=new Scanner(System.in);
    String dv=myscan.nextLine();
        String dv1="";
        String dv2="";
        if(dv.substring(0,1).equals("1")==true){
            dv1="0"+dv.substring(1);
        for(int i=0;i<dv.length()-1;i++)
            dv2+="1";
        System.out.println(Integer.parseInt(dv1,2)-Integer.parseInt(dv2,2)-1);}
        else System.out.println(Integer.parseInt(dv,2));
    }
}



# rust
use std::io::{self, Read};

fn main() {
    // Read the entire input (the binary string)
    let mut input = String::new();
    io::stdin().read_to_string(&mut input).expect("Failed to read input");
    let b = input.trim(); // remove trailing newline characters

    // Parse the binary string as a signed 64‑bit integer
    let value = i64::from_str_radix(b, 2).expect("Input must be a binary number");

    // Get the most significant bit (the first character) as an integer (0 or 1)
    let msb = b
        .chars()
        .next()
        .expect("Input cannot be empty")
        .to_digit(10)
        .expect("First character must be 0 or 1") as i64;

    // Compute the shift amount (length of the binary string)
    let shift = b.len() as u32;

    // Perform the required calculation:
    // value - (msb << shift)
    let result = value - (msb << shift);

    // Output the result
    println!("{}", result);
}





