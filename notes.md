#char *strcpy(char *dest, const char *src) {
  char *save = dest;
  while (*dest++ = *src++);
  return save;
} Execution environment:

. freestanding -- may not provide an OS and is typically used for embedded dev.
. hosted -- provide minimal set of of lib functions.

---

# Five kinds of portability issues:

. Implementation-defined behavior -- not specified by the C Standard, but has consistent, documented behaviour within an implementation. 
. Unspecified behaviour -- is program behavior for which the standard provides two or more options. 
. Undefined behaviour -- is behaviour that isn't defined by the C Standard.
. Locale-specific behaviour -- depends on local conventions of nationality, culture and language.
. Common extensions -- widely used in many systems but not portable to all implementations.

---

. object -> variable (have declared type)
. function (type declared by return value and type and number of parameters) -> pointer (referenced type)

---

# C is call-by-value language

Value of argument provided to function copied into a distinct variable foe use within the function. 

---

# Storage duration

. automatic
. static
. thread
. allocated

---

# Object types

. Boolean types -> `stdbool.h`
. Character types -> [`char`, `signed char`, `unsigned char`] 
  -- wide character `wchar_t` to represent more character than ASCII, range 16 to 32 bits.
. Numerical types:
  . Integer types -> size specified in `limits.h`, actual width integers by using types from `stdint.h` and `inttypes.h`
  . enum types -> allows to define a type that assigns names to int values
  . Floating-Point types -> `float`, `double`, `long double`
  . void types 

---

# Function types

. Depends from return type

---

# Derived types
	Constructed from other types.
. Pointer types -> derived from the function or object types that it points to.
. Arrays
. Structures
. Unions -> memory used by the member objects overlaps, can contain an object of one type at one type, and an object of a different type at different time.

---

# Type qualifiers
. const -> can be placed in read-only memory by the compiler, and any attempt to write to them will result in a runtime error. Undefined behavior:
`const int i = 1;
int *ip = (int *)&i;
*ip = 2;`
. volatile -> used to model memory-mapped I/O ports. The values stored in these objects may change without the knowledge of the compiler.
. restrict -> used to promote optimization.

---

#Arithmetic Types

#Integers

---

. except `char`, `signed char` and `unsigned char` may contain unused bits, called padding.
. width -> the number of bits used to represent a value of a given type, excluding padding but including the sign.
. precision -> is the number of bits used to represent values, excluding sign and padding bits.

---

`limits.h` provides the min and max represented values for the various int types.

`int agent = 007` -> leading `0` turns it into octal value.
`int burger = 0xDEADBEEF` -> leading `0x` turns in into hex value. 

---

#Floating-point

---

#Expressions and operators

. Side effects -> are changes to the state of the execution environment.

# Control Flow

---

. `abort()` function (declared in the `<stdlib.h>` header) causes abnormal program termination, making it easy to detect the error.
. helpful way to use `goto` statements is to chain them together to release allocated resources.

# Dynamically allocated memory

Used when the exact storage requirements for a program are unknown before runtime.
The content of memory returned from `malloc` are uninitialized.

`aligned_alloc` - used to request stricter alignment than the default.

`calloc` - allocates storage for an array of `nmemb` objects.

`realloc` - increases or decreases size of previously allocated storage. Calling `realloc` with a null pointer is equivalent to calling `malloc`.

`reallocarray` - reallocates storage for array, but also provides overflow checking for array size calculations.

`double-free vulnerability`

`alloca` - allows allocate memory on the stack. gcc provides a -Walloca flag and -Walloca-larger-than=size.

`dmalloc` - library that replaces standard functions with routines that provide debugging facilities.

#Characters and strings

`char`

`int`

`wchar_t` can be used to encode other than Unicode encodings.

`char16_t` and `char32_t` - datatypes for Unicode characters.

`L'a'` - `wchar_t`
`u'a'` - `char16_t`
`U'a'` - `char32_t`

gcc flags for strings processing:

`-fexec-charset=charset` -- can be used for any encoding supported by the system's `iconv` library.

`-fwide-exec-charset=charset` -- used for wide execution char set.

`-finput-charset=charset` -- used to set input charset.

#Strings

`string` -- array of chars terminated by `\0`.

`wide string` -- array of `\0` terminated chars.

`char *strcpy(char *dest, const char *src) {
  char *save = dest;
  while (*dest++ = *src++);
  return save;
}`

The `gets` function was deprecated in C99 and eliminated from C11.

Use `gets_s` instead.


#Input/Output
