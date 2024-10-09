# Лабораторная работа 2

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
