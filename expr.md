# expr.c
## rules

* "/"
* "-"
* "*"
* NOTYPE
* "+"
* "("
* ")"
* EQ
* NEQ
* HEX
* AND
* NUM
* OR
* REG

## priority
Operator | Priority
-------- | --------
DEREF | 2
NEG | 2
"*" | 3
"/" | 3
"+" | 4
"-" | 4
EQ  | 7
NEQ | 7
AND | 9
OR  | 9

## make token
main function
```C
bool make_token(char *e)
```
additional definition
```C
Token tokens[65536] __attribute__((used)) = {};
int nr_token __attribute__((used)) = 0;
```
order to switch
* NOTYPE
* NEG
* HEX
* NUM

## expr
definition
```C
uint32_t expr(char *e, bool *success)
```
!> called function: eval()

## eval()
definition
```C
uint32_t eval(int p, int q, bool *success)
```
!> called function: sscanf(), isa_reg_str2val(), check_parentheses(), is_op()

## check_parentheses
```C
bool check_parentheses(int p, int q)
```

