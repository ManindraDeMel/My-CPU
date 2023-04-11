# Custom CPU Design Report with Extended ISA

In this report, we will discuss the design, implementation, and analysis of a custom CPU built using a circuit design program. The custom CPU meets the assignment specifications by providing a unique architecture tailored to optimize performance and efficiency. This custom CPU extends the base ISA with additional ALU operations, logical shifts, and support for both ALU and Memory immediates, while maintaining backward compatibility with the base ISA.

### General benefits

- Additional ALU operations: The extended ISA provides more ALU operations, allowing for a wider range of arithmetic and logical tasks to be performed. This enhances the capabilities of the custom CPU and enables it to handle more complex tasks more efficiently.

- Logical shifts: By using an extra bit for direction in the shift instructions, the custom CPU can perform both left and right shifts, providing greater flexibility in data manipulation. This feature allows for more efficient bit-level operations and can lead to improved performance in certain tasks.

- ALU and Memory immediates: The extended ISA supports immediate values for both ALU and Memory instructions, enabling the custom CPU to perform operations with constant values more efficiently. This feature reduces the need to load values into registers before performing an operation, thus saving clock cycles and improving performance.

### Limitations

- Backward compatibility: The requirement to maintain backward compatibility with the base ISA imposes certain limitations on the design of the custom CPU. It restricts the addition of new instructions or modifications to existing instructions, as doing so might break compatibility with existing programs written for the base ISA. This constraint might result in a suboptimal design for certain tasks or limit the overall performance improvements that could be achieved with a completely new ISA.

## Implementation

The custom CPU uses the following extended ISA while maintaining backward compatibility with the base ISA:

| Syntax                       | Semantic           | Machine Code                      |
| ---------------------------- | ------------------ | --------------------------------- |
| I-Format Instructions        |
| `movl rd, imm8`              | `rd ≔ #imm8`       | `0000 <cond> <rd> <imm8>`         |
| `seth rd, imm8`              | `rd ≔ (#imm8 << 8) | (rd & 0xff)`|`0001 <cond> <rd> <imm8>`|
| I-Format ALU Instructions    |
| `add rd, imm7`               | `rd ≔ rd + #imm8`  | `0011 <cond> <rd> 0 <imm7>`  |
| `sub rd, imm7`               | `rd ≔ rd - #imm8`  | `0011 <cond> <rd> 1 <imm7>`  |
| R-Format Memory Instructions |
| `str rd, [ra]`               | `[ra] ≔ rd`        | `0100 <cond> <rd> 0 <ra> 0000`    |
| `ldr rd, [ra]`               | `rd ≔ [ra]`        | `0101 <cond> <rd> 0 <ra> 0000`    |
| `str rd, [imm7],`               | `[rd] ≔ imm7`      | `0111 <cond> <rd> 0 <imm7>`       |
| `ldr rd, [imm7]`               | `rd ≔ [imm7]`      | `0111 <cond> <rd> 1 <imm7>`       |
| R-Format ALU Instructions    |
| `add rd, ra, rb`             | `rd ≔ ra + rb`     | `1000 <cond> <rd> 0 <ra> 0 <rb>`  |
| `sub rd, ra, rb`             | `rd ≔ ra - rb`     | `1001 <cond> <rd> 0 <ra> 0 <rb>`  |
| `and rd, ra, rb`             | `rd ≔ ra & rb`     | `1010  <cond> <rd> 0 <ra> 0 <rb>` |
| `orr  rd, ra, rb`            | `rd ≔ ra | rb`     | `1011  <cond> <rd> 0 <ra> 0 <rb>` |
| `xor  rd, ra, rb`            | `rd ≔ ra ⊕ rb`    | `1100  <cond> <rd> 0 <ra> 0 <rb>` |
| `not  rd, ra`                | `rd ≔ ~ra`         | `1101  <cond> <rd> 0 <ra> 0000`  |
| `shift rd, ra, rb`           | `rd ≔ ra << rb || rd ≔ ra >> rb`  | `1110 <cond> <rd> 0 <ra> <direction> <rb>` |
| `neg rd, ra`                 | `rd ≔ -1 x ra`     | `1111  <cond> <rd> 0 <ra> 0000` |

One of the key improvements in the extended ISA over the base ISA is the inclusion of more ALU operations, such as XOR, NOT, and NEG. This extended set of operations allows the CPU to perform a wider range of tasks more efficiently, enabling complex arithmetic and bitwise operations that can significantly enhance overall performance.

In addition to the expanded ALU operations, the extended ISA introduces logical shifts with an extra bit to indicate the direction. This provides a more flexible approach to shifting bits in registers, ultimately making it easier to perform tasks such as multiplication, division, or data manipulation.

Another benefit of the extended ISA is the inclusion of both ALU and memory immediates. The ability to use immediate values in ALU and memory instructions simplifies the instruction set and reduces the need for additional load instructions to access immediate values. This can lead to a more efficient execution of the program, as fewer instructions are needed for certain tasks.

## Analysis

The custom CPU design is based on an extended ISA that offers a richer set of ALU operations, logical shifts with direction control, and support for both ALU and memory immediates. These enhancements significantly improve the CPU's ability to execute a wide variety of tasks more efficiently, while maintaining backward compatibility with the base ISA.

In order to accommodate the additional instructions and functionality in the extended ISA, certain modifications were made to the CPU's internal components. These changes were carefully designed to provide the desired functionality while preserving backward compatibility with the base ISA.

The control unit was updated to handle the new instructions and control signals required for the extended ISA. This involved modifying the control logic and adding new state transitions to accommodate the additional functionality. The control unit's design was carefully optimized to balance the need for increased functionality with the desire to maintain a simple and efficient structure.

The instruction decoder was also modified to recognize and decode the new instructions introduced by the extended ISA. This required the addition of new decoding logic and updates to the existing decoding circuits to ensure proper identification and execution of the new instructions.

Throughout the design process, careful consideration was given to the trade-offs between increased functionality, performance, and complexity. The result is a custom CPU that successfully incorporates the benefits of the extended ISA while maintaining backward compatibility with the base ISA, providing a versatile and powerful solution for a wide range of tasks.