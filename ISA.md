| Syntax                       | Semantic           | Machine Code                      |
| ---------------------------- | ------------------ | --------------------------------- |
| I-Format Instructions        |
| `movl rd, imm8`              | `rd ≔ #imm8`       | `0000 <cond> <rd> <imm8>`         |
| `seth rd, imm8`              | `rd ≔ (#imm8 << 8) | (rd & 0xff)`|`0001 <cond> <rd> <imm8>`|
| I-Format ALU Instructions    |
| `add rd, imm8`               | `rd ≔ rd + #imm8`  | `0010 <cond> <rd> <imm8>`  |
| `sub rd, imm8`               | `rd ≔ rd - #imm8`  | `0011 <cond> <rd> <imm8>`  |
| R-Format Memory Instructions |
| `str rd, [ra]`               | `[ra] ≔ rd`        | `0100 <cond> <rd> 0 <ra> 0000`    |
| `ldr rd, [ra]`               | `rd ≔ [ra]`        | `0101 <cond> <rd> 0 <ra> 0000`    |
| R-Format ALU Instructions    |
| `add rd, ra, rb`             | `rd ≔ ra + rb`     | `1000 <cond> <rd> 0 <ra> 0 <rb>`  |
| `sub rd, ra, rb`             | `rd ≔ ra - rb`     | `1001 <cond> <rd> 0 <ra> 0 <rb>`  |
| `and rd, ra, rb`             | `rd ≔ ra & rb`     | `1010  <cond> <rd> 0 <ra> 0 <rb>` |
| `orr  rd, ra, rb`            | `rd ≔ ra | rb`     | `1011  <cond> <rd> 0 <ra> 0 <rb>` |
| `xor  rd, ra, rb`            | `rd ≔ ra ⊕ rb`    | `1100  <cond> <rd> 0 <ra> 0 <rb>` |
| `not  rd, ra`                | `rd ≔ ~ra`         | `1101  <cond> <rd> 0 <ra> 0 000`  |
| `shift rd, ra, rb`           | `rd ≔ ra << rb || rd ≔ ra >> rb`  | `1110 <cond> <rd> 0 <ra> <direction> <rb>` |
| `neg rd`                     | `rd ≔ -1 x rd` | `1111  <cond> <rd> 0 000 0 000` |
