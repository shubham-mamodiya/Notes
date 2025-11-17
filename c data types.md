| Type                      | 32-bit system | 64-bit system       |
| ------------------------- | ------------- | ------------------- |
| `char`                    | 1 byte        | 1 byte              |
| `short`                   | 2 bytes       | 2 bytes             |
| `int`                     | 4 bytes       | 4 bytes             |
| `long`                    | 4 bytes       | **8 bytes** (often) |
| `long long`               | 8 bytes       | 8 bytes             |
| `float`                   | 4 bytes       | 4 bytes             |
| `double`                  | 8 bytes       | 8 bytes             |
| `long double`             | 12 or 16      | 16 (usually)        |
| pointer (`int*`, `char*`) | 4 bytes       | **8 bytes**         |
Got it — you want one single file, but with more details added (not a short/minimal table).
So I’ll produce a complete, detailed, single, continuous file — no splitting, no fences, no interruptions.

You can copy-paste the following as one file (example name: c_all_types_full.md):

C Data Types: Sizes, Ranges, Format Specifiers, and Notes

(Typical 64-bit system, GCC/Clang)

Fundamental Integer Types

Type	Bytes	Bits	Signed Range	Unsigned Range	printf Format

char	1	8	-128 to 127 (if signed char)	0 to 255 (if unsigned char)	%c
signed char	1	8	-128 to 127	—	%hhd
unsigned char	1	8	—	0 to 255	%hhu
short	2	16	-32768 to 32767	—	%hd
unsigned short	2	16	—	0 to 65535	%hu
int	4	32	-2,147,483,648 to 2,147,483,647	—	%d
unsigned int	4	32	—	0 to 4,294,967,295	%u
long	8	64	-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807	—	%ld
unsigned long	8	64	—	0 to 18,446,744,073,709,551,615	%lu
long long	8	64	-9.22e18 to +9.22e18	—	%lld
unsigned long long	8	64	—	0 to 1.84e19	%llu



---

Fixed-Width Integer Types (stdint.h / inttypes.h)

Exact bit-width, same on all systems.

Type	Bytes	Bits	Signed Range	Unsigned Range	printf Format

int8_t	1	8	-128 to 127	—	%" PRId8 "
uint8_t	1	8	—	0 to 255	%" PRIu8 "
int16_t	2	16	-32768 to 32767	—	%" PRId16 "
uint16_t	2	16	—	0 to 65535	%" PRIu16 "
int32_t	4	32	-2^31 to 2^31−1	—	%" PRId32 "
uint32_t	4	32	—	0 to 2^32−1	%" PRIu32 "
int64_t	8	64	−2^63 to 2^63−1	—	%" PRId64 "
uint64_t	8	64	—	0 to 2^64−1	%" PRIu64 "


To print them: #include <inttypes.h>


---

Fast and Least Integer Types (stdint.h)

least types: smallest type with that many bits

fast types: fastest type with at least that many bits


Examples: int_fast8_t, int_fast16_t, int_least32_t, uint_fast64_t

Compilers can choose larger types for speed.


---

Pointer-Sized Integer Types

Type	Bytes	Bits	Purpose

intptr_t	8	64	can store a pointer safely in an integer
uintptr_t	8	64	unsigned version


Used when converting pointers to numbers.


---

Floating-Point Types

Type	Bytes	Bits	Approx Range	Precision	printf

float	4	32	±3.4e38	~6 decimal digits	%f
double	8	64	±1.7e308	~15 digits	%lf
long double	16	128	~1e4932	~18-21 digits	%Lf



---

Boolean Type

Type	Bytes	Bits	Values	printf

_Bool / bool	1	8	0 or 1	%d


Requires: #include <stdbool.h>


---

Pointer Types

Type	Bytes	Bits	printf

any pointer (int*, char*, void*, struct*)	8	64	%p



---

Size and Address Types

Type	Bytes	Meaning	printf

size_t	8	size of objects/arrays	%zu
ssize_t	8	signed size	%zd
ptrdiff_t	8	result of pointer subtraction	%td
time_t	usually 8	seconds	%ld or %lld
clock_t	usually 8	CPU ticks	%ld



---

enum

stored as int (4 bytes on most systems)

printed using %d



---

struct and union

struct size = sum of fields + alignment padding

padding inserted to align data for fast access

union size = size of largest member


Example: struct A { char a; int b; };
Often becomes 8 bytes because compiler adds padding after a.


---

Strings

stored as arrays of char

end with '\0'

printing: %s → string
%c → one character


Examples: char name[20];
char *p = name;


---

Wide Characters (wchar.h)

Type	Bytes	Bits	printf

wchar_t	4	32	%lc or %ls
wint_t	4	32	for wide characters in functions



---

Special Values

NULL → null pointer
'\0' → null character, string terminator
0 → integer zero


---

Quick Master Size List (Memory Cheat Sheet)

char – 1 byte
short – 2 bytes
int – 4 bytes
long – 8 bytes
long long – 8 bytes
bool – 1 byte
float – 4 bytes
double – 8 bytes
long double – 16 bytes
any pointer – 8 bytes
int8_t – 1
int16_t – 2
int32_t – 4
int64_t – 8
intptr_t – 8


---

Notes for Portability

sizes above are for 64-bit systems; 32-bit systems change pointer, long, size_t (4 bytes)

use sizeof(type) to get actual system sizes

for printing fixed-width integers, always use inttypes.h macros



exact numeric limits using INT_MAX, UINT_MAX, emacros from <limits.h> and <float.h>.




