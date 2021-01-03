Assembly
===


## 常見指令

```
mov bl, byte ptr [rbx] 		; char bl = *(char *)rbx
							; [] 代表取值

; lea 拿後面東西的位置
lea rax, [0x12345678]		; rax = 0x12345678
							; [] 取值，lea 取值，取值又取值就回到原本的樣貌

lea rax, [rax*2 + 16]		; rax = rax * 2 + 16
							; mov 無法直接做到這樣的數值運算，速度可以比較快

mov eax, 20
mov ecx, 3
mul ecx						; edx:eax = eax * ecx
div ecx						; edx:eax / 3 。商放 eax, 餘數放 edx


nop 						; xchg eax, eax 也就是啥都不做

shl rax, 2					; rax = rax << 2

shr rax, 2					; rax = rax >> 2

not rax						; rax = !rax

neg rax						; rax = -rax (2 的補數)


test rax, rbx				; rax & rbx ，結果寫到 EFLAGS(x86) or RFLAGS(x64)

cmp rax, rbx				; rax - rbx ，結果寫到 EFLAGS(x86) or RFLAGS(x64)

```


## FLAGS Register

- Zero Flag
	- 結果為 0 就會 ZF = 1
	- EX: 100 - 100 = 0
- Carry Flag
	- 最高的 bit 借位(溢位)或進位(溢位)
	- 用無號整數去看
	- ex: 0 - 1 = 4294967295
		- CF = 1 ，因為你往外面借位 (往不存在的 32 bit 借位)
	- ex: 4294967295 + 1 = 0
		- CF = 1 ，因為你往不存在的 32 bit 進位
- Overflow Flag
	- 用有號整數去看
	- overflow 時，設值為 1
		- 用加法加到變成負的，或是減法減到變成正的
		- ex: 2147483647 + 1 = - 2147483648
- Sign Flag
	- 如果運算結果為負，就會設值為 1
	- ex: 0 - 1 = - 1
	- 其實就是看最高位 (sign bit)

比對的時候不會管有號還是無號，Flags register 會設定好

由 Jcc 決定是看有號或無號

假設： `cmp eax, ebx`


**無號整數**
| ZF | CF | 結果 |
| :---:         |     :---:      |          :---: |
| False   | True     | eax < ebx    |
| False     | False       | eax > ebx      |
| True     | False       | eax == ebx      |



**有號整數**
| EFLAG |  結果 |
| :---:              |          :---: |
| Sign flag != Overflow flag |eax < ebx|
|Sign flag == Overflow flag|eax > ebx|
|ZF = True |eax == ebx|


結果是大於
- 有號：JG
- 無號：JA

結果是小於
- 有號：JL
- 無號：JB






38:52

