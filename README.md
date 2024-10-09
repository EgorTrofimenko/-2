# Лабораторная работа 2
Для выполнения данной лабораторной работы, я определил задачу и изучил синтаксис языка программирования Bash, а именно то, что касается условных операторов if, цикла for, а так же работы с переводом чисел из десятитчной в двоичную систему исчисления и разделения строк.
После этого я начал писать код, который проверяет строку на то, что она соответствует формату IPv-4, разделяет строку на отдельные числа в тех местах, где стоит знак ".", потом проверяет, что числовое значение числа не превышает 255 и, если это правда, то переводит его в двоичное число, а если нет, то выводит сообщение о том, что IP адрес введен неверно(то же самое программа делает в случае прочих несоответствий формату IPv-4).

```bash
#!/bin/bash
IFS="."
read -p "Введите IP:" ip
res=""
if [[ $ip =~ ^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}$ ]]
then
  for i in $ip; do
    if [[ $i -le 255 ]]
    then
      a="$((`echo "obase=2;$i" | bc`))"
      b="${#a}"
      if [[ b -eq 8 ]]
      then
        res+="$a."
      else
        for (( i=0; i <= 7-$b; i++))
        do
          res+="0"
        done
        res+="$a."
      fi   
    else
      unset res
      res="IP is incorrect."
      break
    fi
  done
  echo "${res::-1}"
else
  echo "IP is incorrect"
fi
```
