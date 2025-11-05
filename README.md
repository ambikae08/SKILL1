# SKILL1_MPMC_AMBIKA

## Aim
To write an **8086 assembly language program** to **count the number of even and odd numbers** in an array of 10 elements and **display the counts** on the screen.

## APPARATUS REQUIRED

Personal computer with masm software

## ALGORITHM

1. Start the program.  
2. Initialize the **data segment** and load the array of numbers.  
3. Set up two memory locations to store **even count** and **odd count**.  
4. Load the base address of the array into **SI register**.  
5. Set **CX = number of elements (10)**.  
6. For each element in the array:
   - Move the number into **AL**.
   - Check the least significant bit (LSB) using `AND AL, 01H`.
   - If the result is **0**, it’s **even** → increment `EVEN_COUNT`.
   - If the result is **1**, it’s **odd** → increment `ODD_COUNT`.
7. Continue until all elements are processed.  
8. Display the count of even and odd numbers using DOS interrupt `INT 21H`.  
9. Stop the program.

## PROGRAME
```
DATA SEGMENT
ARR DB 07,08,05,04
EVEN_COUNT DB 0
ODD_COUNT DB 0
MSG1 DB 13,10,'Number of Even Numbers = $'
MSG2 DB 13,10,'Number of Odd Numbers = $
DATA ENDS

CODE SEGMENT
ASSUME DS:DATA, CS:CODE

START:
MOV AX, DATA
MOV DS, AX

MOV SI, OFFSET ARR
MOV CX, 10

NEXT_NUM:
MOV AL, [SI]
MOV BL, AL
AND BL, 01H
CMP BL, 00H
JZ EVEN_LABEL

ODD_LABEL:
INC ODD_COUNT
JMP CONTINUE

EVEN_LABEL:
INC EVEN_COUNT

CONTINUE:
INC SI
LOOP NEXT_NUM

; ----- Display results
MOV AH, 09H
LEA DX, MSG1
INT 21H

MOV AL, EVEN_COUNT
CALL DISP_NUM

MOV AH, 09H
LEA DX, MSG2
INT 21H
MOV AL, ODD_COUNT
CALL DISP_NUM

MOV AH, 4CH
INT 21H

; ===== Subroutine to display number in AL =====
DISP_NUM PROC
ADD AL, 30H
MOV DL, AL
MOV AH, 02H
INT 21H
RET
DISP_NUM ENDP

CODE ENDS
END
```
## OUTPUT

<img width="627" height="386" alt="Screenshot 2025-11-05 082603" src="https://github.com/user-attachments/assets/7c10ee63-560c-490e-9d26-13105ce409ba" />

<img width="626" height="385" alt="Screenshot 2025-11-05 082619" src="https://github.com/user-attachments/assets/838cf1f4-8f43-468c-9e75-76608812ac75" />

<img width="632" height="381" alt="Screenshot 2025-11-05 082546" src="https://github.com/user-attachments/assets/d6f1d16f-08f7-469a-b246-eef240b96314" />

<img width="637" height="397" alt="Screenshot 2025-11-05 083228" src="https://github.com/user-attachments/assets/3400317a-7806-46e6-85a7-1a008da1af5f" />

## RESULT

The 8086 Assembly Program successfully counts and displays the number of even and odd numbers in the given array of 10 elements.
