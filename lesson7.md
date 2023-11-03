Бинарные уязвимости
Урок 10. Видеоурок 7 "Внутреннее устройство шелл-кода"

Сформировать эксплойт для программы prog4d. В качестве полезной нагрузки необходимо использовать шелл-код test_shell4.c.
```clang
$ cat prog4d.c 
#include <stdio.h>
#include <string.h>

void vuln_func(char *data) { 
  char buff[128]; 
  strcpy(buff, data); 
} 

void main(int argc, char *argv[]) {
    vuln_func(argv[1]);
}

$ cat ../0x07.03/test_shell4.c 
#include <stdio.h>
#include <string.h>

unsigned char shellcode[]=
"\x31\xc0\xb0\x04\x31\xdb\xb3\x01"
"\x68\x21\x0a\x41\x41\x68\x6f\x72"
"\x6c\x64\x68\x6f\x2c\x20\x57\x68"
"\x48\x65\x6c\x6c\x89\xe1\x31\xd2"
"\xb2\x0e\xcd\x80\x31\xc0\xb0\x01"
"\x31\xdb\xcd\x80";

void main() {
  printf("Shellcode Length: %d\n", strlen(shellcode));
  int (*ret)() = (int(*)())shellcode;
  ret();
}
```
Выполнение: 
