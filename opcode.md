# Operation Code
## opcode_table
|imm01|b000|b001|b010|b011|b100|b101|b110|b111|
|-----|----|----|----|----|----|----|----|----|
| b00| ld,[load](#load)| EMPTY| EMPTY| EMPTY| Mathi,[mathi](#mathi)| U,auipc| EMPTY| EMPTY|
| b01| st,[store](#store)| EMPTY| EMPTY| EMPTY| Math,[math](#math)| U, lui| EMPTY| EMPTY|
| b10| EMPTY| EMPTY| EMPTY| EMPTY| EMPTY| EMPTY| EMPTY| EMPTY|
| b11| BQ,[bq](#bq)| JR,<span id="jr">jr</span>| nemu_trap| J,<span id="jal">jal</span>| EC,ec| EMPTY| EMPTY| EMPTY|

## func3 table
|direct|b000|b001|b010|b011|b100|b101|b110|b111|
|-----|------|------|------|----|----|----|----|----|
|<span id="load">load</span>| ldd,1| ldd,2| ldd,4| EMPTY| ld,1| ld,2| ld,4| EMPTY|
|<span id="store">store</span>| st,1| st,2| st,4| EMPTY| EMPTY | EMPTY| EMPTY| EMPTY |
|<span id="math">math</span>| [add](#add),4| [sl](#sl),4| <span id="slt">slt</span>,4| [sltu](#sltu),4| [div](#div),4| [sr](#sr),4| [rem](#rem),4| [and](#and),4|
|<span id="mathi">mathi</span>| <span id="addi">addi</span>,4| slli,4| slti,4| <span id="sltiu">sltiu</span>,4| <span id="xori">xori</span>,4| [srai](#srai),4| srli,4| andi,4|
|<span id="bq">bq</span>| <span id="beq">beq</span>,4| <span id="bne">bne</span>,4| EMPTY| EMPTY| <span id="blt">blt</span>,4| <span id="bge">bge</span>,4| <span id="bltu">bltu</span>,4| <span id="bgeu">bgeu</span>,4|

## EHelpers with func7
* <span id="srai">***srai***</span>
  - func7 =  0 : rtl_sari (srli)
  - func7 =  1 : 
  - func7 = 32 : rtl_shri (srai)

* <span id="add">***add***</span>
  - func7 =  0 : rtl_add (add)
  - func7 =  1 : rtl_mul_lo (mul)
  - func7 = 32 : rtl_sub (<span id="sub">sub</span>)

* <span id="sr">***sr***</span>
  - func7 =  0 : rtl_shr (srl)
  - func7 =  1 : rtl_idiv_q (div)
  - func7 = 32 : rtl_sar (sra)

* <span id="sl">***sl***</span>
  - func7 =  0 : rtl_shl (sll)
  - func7 =  1 : rtl_imul_hi (nulh)
  - func7 = 32 : 

* <span id="div">***div***</span>
  - func7 =  0 : rtl_xor (xor)
  - func7 =  1 : rtl_div_q (divu)
  - func7 = 32 : 
  
* <span id="rem">***rem***</span>
  - func7 =  0 : rtl_or (or)
  - func7 =  1 : rtl_idiv_r (rem)
  - func7 = 32 : 

* <span id="sltu">***sltu***</span>
  - func7 =  0 : sltu
  - func7 =  1 : rtl_mul_hi (mulhu)
  - func7 = 32 : 

  
* <span id="and">***and***</span>
  - func7 =  0 : rtl_and (and)
  - func7 =  1 : rtl_div_r (remu)
  - func7 = 32 : 

  
## pseudo instruction
beqz -> [beq](#beq) rs1, x0, offset
bgez -> [bge](#bge) rs1, x0, offset
bgt -> [blt](#blt) rs2, rs1, offset
bgtu -> [bltu](#bltu) rs1, x0, offset
bgtz -> [blt](#blt) x0, rs2 offset
ble -> [bge](#bge) rs1, x0, offset
bleu -> [bgeu](#bgeu) rs2, rs1, offset
blez -> [bge](#bge) x0, rs2, offset
bltz -> [blt](#blt) rs1, x0, offset
bnez -> [bne](#bne) rs1, x0, offset

j -> [jal](#jal) x0, offset
jr -> [jalr](#jalr) x0, 0(rs1)
li -> [addi](#addi) rd, x0, immediate
mv -> [addi](#addi) rd, rs1, 0
neg -> [sub](#sub) rd, x0, rs2
not -> [xori](#xori) rd, rs1, -1
ret -> [jalr](#jr) x0, 0(x1)
seqz -> [sltiu](#sltiu) rd, rs1, 1
sgtz -> [slt](#slt) rd, x0, rs2
sltz -> [slt](#slt) rd, rs1, x0
snez -> [sltu](#sltu) rd, x0, rs2






 