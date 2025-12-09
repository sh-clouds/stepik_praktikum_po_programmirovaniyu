Universal convertor

Напишите программу, переводящую запись числа между двумя произвольными системами счисления.

Входные данные
На вход программа получает три величины: n, A, k, где n и k — натуральные числа от 2 до 36, основания системы счисления, A — число, записанное в системе счисления с основанием n, A < 
2
31
2 
31
 .

Выходные данные
Необходимо вывести значение A в системе счисления с основанием k без лидирующих нулей.

Цифры записываются следующими символами: 0, 1, 2, ..., 9, A, B, C, ..., Z.

Sample Input 1:

10
19
2
Sample Output 1:

10011
Sample Input 2:

10
32
3
Sample Output 2:

1012
Напишите программу. Тестируется через stdin → stdout
Верно решили 64 учащихся
Из всех попыток 45% верных


# ruby
n, a, k = Array.new(3) { gets.chomp }
puts a.to_i(n.to_i).to_s(k.to_i).upcase


# python
def convert(num, from_base=10, to_base=10):
    digs = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ'
    num = int(num, from_base)
    res = []
    while num:      
        res.append(digs[num % to_base])
        num //= to_base 
    return(''.join(reversed(res)))

n, a, k = map(str.strip, open(0))
print(convert(a, int(n), int(k)))


# C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Numerics;

public class MainClass
{
    public static void Main()
    {
        int n = int.Parse(Console.ReadLine());
        string A = Console.ReadLine();
        int k = int.Parse(Console.ReadLine());
        string rez = "";
        string c = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        long dec = 0;
        for (int i = 0; i < A.Length; i++) {
            dec += c.IndexOf(A[i]) * (long)Math.Pow(n, A.Length - i - 1);
        }
        for (int i = 0; dec > 0; i++) {
            rez = c[(int)(dec % k)] + rez;
            dec /= k;
        }
        Console.WriteLine(rez);
    }
}


# java
import java.util.Scanner;
import java.util.ArrayList;
class Main {
    public static void main(String[] args) {
Scanner v=new Scanner(System.in);
int nachSistema=v.nextInt();v.nextLine();
String aHislo=v.nextLine(); 
int konSistema=v.nextInt(),chet=0; long sistema10=0; 
ArrayList <String> vasList=new ArrayList();        
if(nachSistema!=10){
    String []str=(aHislo).split("");
    int []vas=new int [str.length];
    for(int i=0;i<str.length;i++){
        char z= str[i].charAt(0);
        if(Character.isDigit(z)==false){
            chet=z-'7';
            vas[i]=chet;
        }  
        else{
            vas[i]=z-'0';
        }
    }
    for(int i=0,j=vas.length-1;i<vas.length;i++,j--){
        sistema10+=vas[i]*(long)Math.pow(nachSistema,j);
    }
} 
else{
    sistema10=Integer.parseInt(aHislo);
} //Переводим из любой начальной системы в десятичную
if(konSistema==10){
    System.out.println(sistema10);
} //Если итоговая система и есть 10 то выводим ответ
else{
    for(long i=sistema10;;){
        if(i<konSistema){
            if(i>9){   
            char perevodFinal=(char)(i+55);
            vasList.add(""+perevodFinal);    
            }
            else{
                vasList.add(""+i);
            }
            break;
        }
        if(i%konSistema>9){
            char perevod=(char)(i%konSistema+55);   
            vasList.add(""+perevod);
            i=i/konSistema;
        }
        else{    
            vasList.add(""+(i%konSistema));
            i=i/konSistema;
        }
    }
    for(int i=vasList.size()-1,br=0;i>=0;i--){
        if(vasList.get(i).equals("0")==false&&br==0){
            br=1;
        }    
        if(br>0){
            System.out.print(vasList.get(i));
        }
    }
}
    }
}


# C++
#include <iostream>
#include <string>
#include <vector>
using namespace std;

int main()
{
    int K, T; // Основание систем счисления
    string bin_number; // Исходное число в виде строки
    cin >> K >> bin_number >> T;
    // Шаг 1. Перевод в десятичную систему счисления
    unsigned long long result(0), // результат перевода
                    Stepen(1);    // степени 
    int d; // очередная цифра числа 
    char s; // Очередная цифра числа в k-ричной системе счисления
    for(int i = bin_number.length()-1; i >=0 ; i--)
    {
        // Простой перевод цифры из символа в число как разность кодов
        s = bin_number[i];
        if (s >= '0' and s <= '9') d = s - '0';
        else d = 10 + s - 'A';
        result += d * Stepen;
        Stepen *= K;
    }
    
    // Шаг 2. Перевод из десятичной системы счисления в T-ричную
    vector<char> V; // Массив цифр числа
    if (result == 0) V.push_back('0');
    while (result)
    {
        // Добавляем очередную цифру в вектор
        d = result % T;
        if (d<10) s = '0' + d;
        else s = 'A' + d - 10;
        V.push_back(s);
        result /= T;
    }
    // Выводим вектор цифр в обратном порядке
    for(auto p = V.rbegin(); p!=V.rend(); p++)
    {
        cout << *p;
    }
    cout << endl;
}