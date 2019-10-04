# User Interface
## cmd_si
```shell
(nemu) si
// execute once, arg default to one
(nemu) si 4
// execute four times
```
!> function ****cpu\_exec()**** is called

## cmd_c
continue executing

## cmd_q
exit NEMU

## cmd_info
now support two commands
```shell
(nemu) info r
// display the values of registers
(nemu) info w
// display info of watchpoints
```
!> function ****isa_reg_display()****, list_watchpoints are called
?> arg is extracted from the command by ****strtok****, other forms or not given will lead to unpleasant responds

## cmd_p
to process the expression
```shell
(nemu) p (1+3*4*(a0+7)) //sample expression
```
!> function ****expr()**** is called to evaluate, may cause "invalid expression error"

## cmd_x
to scan the momory and print adjacent cache
```shell
(nemu) x 10 0x800000
```
!> the first arg parsed by built-in function ****atoi()****, and the second one passed to function ****vaddr_read()****

!> known issue: break down unexpectedly after x command at 0x800000

## cmd_w
```shell
(nemu) w a0 // watchpoint at register
(nemu) w 0x800000 // watchpoint at memory
```
!> function ****set_watchpoints()**** is called to parse string directly

## cmd_d
delete a watchpoint
```shell
(nemu) d 1 // delete watchpoint NO.1
```
!> function ****del_watchpoint()**** is called, but if more args than one are given, only the first one will be processed. args be transformed to integer by ****sscanf()**** built-in function

## cmd_help
show help for other funcions
```shell
(nemu) help si
```
