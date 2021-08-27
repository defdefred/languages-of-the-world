# languages of the world
## written langage
ISO 15924 tells us that there is only 210 codes to covers all writing systems.

https://unicode.org/iso15924/iso15924.txt
```
$ wc -l iso15924.txt
210 iso15924.txt
```
A full byte is enough and allow new one to be added (256-210=46).

So why using:
- this 4 letters code (26x26x26x26=456976)
- and numerical range 000->999 ?

Let's convert the 4 letters code to pure numerical value:
https://github.com/defdefred/languages-of-the-world/blob/main/iso15924.csv

The code used is:
```
cat iso15924.txt | while IFS=\; read CODE NUM TXT ; do
        A1=$(printf '%d' "'$(echo $CODE |cut -c 1)")
        A2=$(printf '%d' "'$(echo $CODE |cut -c 2)")
        A3=$(printf '%d' "'$(echo $CODE |cut -c 3)")
        A4=$(printf '%d' "'$(echo $CODE |cut -c 4)")
        VAL=$(echo "($A1 - 65) * ( 26*26*26 ) + ( $A2 - 97 ) * ( 26 * 26 ) + ( $A3 - 97 ) *  26 + ( $A4 - 97 )" | bc)
        echo "$VAL;$CODE;$NUM;$TXT"
done
```
## spoken language
ISO 639-3 tells us that there is 7893 codes to covers all referenced languages.

https://iso639-3.sil.org/code_tables/download_tables#Complete%20Code%20Tables
```
$ wc -l iso639-3.txt
7893 iso639-3.txt
```
A full byte is enough for all most used language and another optional byte is more than enough for the others (65536-7893=57643).

So why using a 3 letters code (26x26x26=17576)

A solution could be 2 bytes written as hexadecimal number 0000->FFFF.

