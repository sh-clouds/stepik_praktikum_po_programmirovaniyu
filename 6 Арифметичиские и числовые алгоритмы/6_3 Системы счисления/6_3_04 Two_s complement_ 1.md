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

