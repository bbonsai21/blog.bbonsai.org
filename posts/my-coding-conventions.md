# My coding conventions - what, why, how

I use *slightly* different conventions based off the programming language I'm using. OOP will not have the same
rules that other langs might have.

# General rules

- Obvious methods/functions MUST NOT have any comment ( e.g. getters, setters ), so that no vertical space is wasted.
<br>
- Anything else must have multi-line comments (even if on 1 singe line), so it's detected
by the LSP. Comments must shortly describe what the function does and how it behaves.
<br>
- Statement evaluation always uses parentheses, even if the language deems them optional. Whenever round brackets are opened, whatever is inside
shall be separeted by 1 space from the brackets (e.g. `( arg1, arg2, arg2 )` ), with commas between arguments touching the preceding one but not
the upcoming one.
<br>
- Statement bodies start always 2 lines below the statement first line, meaning that the opening curly brace is always placed 1 line below the
first statement line. E.g.

```C
if ( isAlive() )
{
        do_whatever();
}
```

- If a language allows for classes to be in the same file, that should be absolutely avoided. 1 file, 1 class. This works especially for Lua,
where we don't really have classes but we can emulate them with a bit of metatables tweaking.

- If a language allows for Java-like *static* methods, and if the language allows it, the constructor should not be used, but instead direct
calls to the static methods should be made (e.g. Math.pow(); that'd be foul, pointless and confusing to be allowed to do Math m = new Math()).
If possible, enforce via a private constructor.

# C
1. variables
- any: **snake_case**
<br>
**Reason**: traditional. Makes words easy to read if compared to Hungarian notaton or PascalCase or camelCase (putting close letters together
can be problematic if final letters of a word look similar to initial letters of the next one; e.g. ballLoad ).

- globals: **g_snake_case** (e.g. g_gravity)
<br>
**Reason**: easily recognisable global variables.

- constants: **SCREAMING_SNAKE_CASE**
<br>
**Reason**: easily recognisable constant variables.

- global constants: **G_SCREAMING_SNAKE_CASE**
<br>
**Reason**: obvious union of the previous 2. Immediate recognition.

2. structs
- any: **snake_case_s** (e.g. my_file_s)
<br>
**Reason**: immediately recognisable struct. 

- particular note: it's opportune for linked lists to have members named *NODE*, for common implementation purposes and easily recognisable
functionality.
<br>
3. functions:
- any: **snake_case()**
<br>
**Reason**: it pretty much is a stradition but, to be fair, this is the most breakable rule. I also happen name functions in PascalCase,
particularly special functions (e.g. Update, Start, etc.), that do important tasks. Use whatever, tbf.

- getters/setters: **get_snake_case()**/**set_snake_case()**
<br>
**Reason**: easily recognisable.

- boolean getter: **is_snake_case()** (**is** prefix + snake_case; e.g. `isBlack()`).
<br>
**Reason**: certain and easily recognisable return type.
<br>
4. misc:
- enums: **SCREAMING_SNAKE_CASE**
<br>
**Reason**: easily recognisable. They are pretty much constants, no fancy stuff like in java.
- custom types (via **typedef**): **snake_case_t**.
<br>
**Reason**: easily recognisable. Sometimes also PascalCase works, or even **SCREAMING** style (e.g. the famous stdlib *FILE* type).


# Lua

I generally apply the same rules as in C, but for **metatables** I prefer prefixing them with meta (e.g. meta_Customer).

# Java

1. variables:
- any: **camelCase**
<br>
**Reason**: common pattern and allows easy writing, opposed to PascalCase. I'll admit I prefer snake_case, but it'd be against common standards
and, therefore, it would come off weird.

- `final`: **SNAKE_CASE**
<br>
**Reason**: allows to distinguish immediately a constant.

- `static`: **g_camelCase**
<br>
**Reason**: allows to distinguish immediately a global.

- `static` `final`: **G_PASCAL_CASE**
<br>
**Reason**: allows to distinguish immediately a global constant (notice the order is precise: first **static**, then **final**).

2. methods:
- any: **camelCase()** (ideally the first word is a verb - e.g. *calculateSum()*).
Ideally, all the attributes/modifiers should be placed above the method's name, so
that it doesn't elongate excessively horizontally. E.g.:

```
public static void
main( String[] args )
```

**Reason**: maintains the flow of the latest written letters, that typically are lower-case. E.g. Math.pow(); 
<br>
- getter/setter: **getCamelCase()** XOR **setCamelCase()**
<br>
**Reason**: maintains the flow and it's pretty spread as convention. Knowing the name of the parameter, you know the getter/setter.
<br>
- boolean getter: **isCamelCase()** XOR **hasCamelCase()** (e.g. *isAlive()*, *hasFood()* )
<br>
**Reason**: helps to immediately recognise the type and flows well inside of statements (e.g. `if ( isFood() ) {...}` )
<br>
3. classes:
- any: PascalCase
<br>
**Reason**: convention + immediately easily distinguishable from variables and methods.
<br>
- `abstract`: **_ClassNamePascalCase**
<br>
**Reason**: immediately distinguishable from other types of classes and doesn't allow mistakes in absence of an LSP.
<br>
- `interface`: **underscore** and -**able** suffix (e.g. *_Retrievable*, *_Runnable*)
<br>
**Reason**: being a type of abtract class, the underscore is inherited. Being that it expresses a "contract", it allows (-able), and forces,
the implementing class to use certain methods
<br>
4. complementary:
- enums: **CAPS_SNAKE_CASE**
<br>
**Reason**: they are logically similar to constants, although with some minor differences. Still allows to narrow down the type.
<br>
