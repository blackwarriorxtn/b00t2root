---
layout: post
title: SarCTF DeepDive
subtitle: extracting different types of nested archives(tar,gz,xz,zip)
tags: [ctf, misc, writeups,bash]
---

* **Category:** Misc
* **Points:** 1000
* **file:** [deepdive](flag.txt)

 
# Solution

since there is a lot of nested archives there is no way that u can extract them manually unless u want to spend 10hrs , so i made this script 


``` 
#!/bin/bash

isflag=$(file flag.txt | grep asci| wc -l)
while [ $isflag -eq 0 ] 
do
    echo "Looking for flag";  
    iszip=$(file * |grep "ip archive" |wc -l )
    if [ $iszip -eq 1 ]; then
        echo "Found a zip"
        cp flag.txt flag.zip
        unzip flag.zip
        rm flag.zip

        

    fi

    istargz=$(file * |grep gz | wc -l)
    if [ $istargz -eq 1 ]; then
        echo "Found gz"
        mv flag.txt flag.gz
        gunzip flag.gz
        mv flag flag.txt


    fi

    isxz=$(file * |grep XZ | wc -l)
    if [ $isxz -eq 1 ]; then
        echo "Found xz"
        tar xf flag.txt
    fi

    istar=$(file * |grep tar | wc -l)
    if [ $istar -eq 1 ]; then
        echo "Found tar"
        tar xf flag.txt
    fi

    bz2=$(file * |grep bz | wc -l)
    if [ $bz2 -eq 1 ]; then
        echo "Found bz2"
        mv flag.txt flag.txt.bz2
        bunzip2 flag.txt.bz2
    fi

    isflag=$(file flag.txt |grep asci | wc -l)
done

```
the script is very simple , it just looks for the file type and if there is a match it will do the work ! 
thats it running the script will simply print out the flag
