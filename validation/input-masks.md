# Input Masks

### Syntax

```
Mask Character	Meaning
A	character of the Letter category required, such as A-Z, a-z.
a	character of the Letter category permitted but not required.
N	character of the Letter or Number category required, such as A-Z, a-z, 0-9.
n	character of the Letter or Number category permitted but not required.
X	Any non-blank character required.
x	Any non-blank character permitted but not required.
9	character of the Number category required, e.g 0-9.
0	character of the Number category permitted but not required.
D	character of the Number category and larger than zero required, such as 1-9
d	character of the Number category and larger than zero permitted but not required, such as 1-9.
#	character of the Number category, or plus/minus sign permitted but not required.
H	Hexadecimal character required. A-F, a-f, 0-9.
h	Hexadecimal character permitted but not required.
B	Binary character required. 0-1.
b	Binary character permitted but not required.
```

### Meta Characters

```
Meta Character	Meaning
>	All following alphabetic characters are uppercased.
<	All following alphabetic characters are lowercased.
!	Switch off case conversion.
;c	Terminates the input mask and sets the blank character to c.
[ ] { }	Reserved.
\	Use \ to escape the special characters listed above to use them as separators.
```

### Code Examples

```cpp
//Example of implementing inputMask
void MainWindow::setInputMask()
{
  //Cant do special characters with an input mask ??
  m_lineEdit->setInputMask(">AAA<aaa!99999nnnnnnnnnn");
}
```
