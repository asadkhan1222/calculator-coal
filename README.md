# calculator-coal

# Objective;
The prime objective of building a calculator in assembly language is to perform a number of calculations in response to user supplied input. This project work also focused principally on numbers and arithmetic operation. To determine and understand the current procedures employed in computer with regard to the calculator. To design a simple calculator that ensure timely processing, To reduce the problems immensely and provides a release working environment.

# Theory:
To particularilize the matter and concept ‘we are going to design a calculator in assembly language. Inherent in the design of the simple calculator, the purpose of this project is to provide on overview of the simple design calculator. Basically a calculator is a person who performs arithmetic and other mathematical calculations Finally, the goal of work is to improve the speed of the simple calculator in such a way that it will maximize the hardware needed and reduce the cost and complexity of the machine. This will help us to enjoy the anticipated high speed of our calculator.Basically, calculator in assembly language will help us to understand the different variety of commands , instructions and help us to gain intellectual knowledge through learning .This project allows to solve complicated problems quickly and in an efficient manner. Additionally it can reduce the problem to simpler tasks and allow the user to devote more time in understanding the problem.

# Implementation;
; model small tells the assembler that you intend to use the small memory model

.MODEL SMALL

;stack 100h reserves 100h bytes for stack.

.STACK 100H

;A data definition statement sets aside storage in memory for a variable, with an optional name

.DATA

MAIN_MENU DB ,0DH,0AH,"Calculator",0DH,0AH

  DB "Press 'A' For ADDITION",0DH,0AH 
  
  DB "Press 'S' For SUBTRACTION",0DH,0AH 
  
  DB "Press 'M' For MULTIPLICATION",0DH,0AH 
  
  DB "Press 'D' For DIVISION",0DH,0AH 
  
  DB "Press 'E' For EXIT",0DH,0AH 
  
  DB "Press 'R' For RETURN to Main Menu",0DH,0AH 
  
  DB "***********",0DH,0AH 
  
  DB "***********",0DH,0AH 
  
  DB "Enter Your CHOICE",0DH,0AH,'$' 
NUM1 DB "Enter First Number",0DH,0AH,'$'

NUM2 DB ,0DH,0AH,"Enter Second Number",0DH,0AH,'$' ADD1 DB ,0DH,0AH,"FOR ADDITION",0DH,0AH,'$'

SUB1 DB ,0DH,0AH,"FOR SUBTRACTION",0DH,0AH,'$'

MUL1 DB ,0DH,0AH,"FOR MULTIPLICATION",0DH,0AH,'$'

DIV1 DB ,0DH,0AH,"FOR DIVISION",0DH,0AH,'$'

EX DB ,0DH,0AH,"GOOD BYE AND HAVE A NICE TIME :)",0DH,0AH,'$'

ANS DB ,0DH,0AH,"ANSWER ",0DH,0AH,'$' CONTINUE DB ,0DH,0AH,"DO YOU WANT TO CONTINUE",0DH,0AH,'$'

OP1 DB ? OP2 DB ?

  Operand DB ? 
  
  CON DB ? 
.CODE

.STARTUP

START:

MOV AH,09H

MOV DX, OFFSET MAIN_MENU

;int21h means that you are using function 01h of the Interrupt type 21.

INT 21H

MOV AH,01H

INT 21H

;The CMP instruction compares two operands.

CMP AL,'A'

; "je" (jump-if-equal), does a goto somewhere if the two values satisfy the right condition.

JE _ADD

CMP AL,'S'

JE _SUB

CMP AL,'M'

JE _MUL

CMP AL,'D'

JE _DIV

CMP AL,'R'

JE START

CMP AL,'E'

JE EXIT

_ADD: ; PERFORMING THE ADDITION

MOV AH,09H

;Offset is basically the distance from the segment point.

MOV DX,OFFSET ADD1

INT 21H

;FIRST OPERAND

MOV AH,09H

MOV DX,OFFSET NUM1

;int21h means that you are using function 01h of the Interrupt type 21.

INT 21H

MOV AH,01H

INT 21H

MOV OP1,AL

;SECOND OPERAND

MOV AH,09H

MOV DX,OFFSET NUM2

INT 21H

MOV AH,01H

INT 21H

MOV OP2,AL

MOV AH,09H

MOV DX, OFFSET ANS

INT 21H

MOV AL,OP1

MOV BL,OP2

ADD AL,BL

AAS

OR AX, 3030H

; PRINT RESULT

MOV AH,0EH

INT 10H

;FOR CONTINUE

MOV AH,09H

MOV DX,OFFSET CONTINUE

INT 21H

MOV AH,01H

INT 21H

CMP AL,'Y'

JE START

CMP AL,'E'

JE EXIT

_SUB: ; PERFORMING SUBTRACTION

MOV AH,09H

MOV DX,OFFSET SUB1

INT 21H

;FIRST OPERAND

MOV AH,09H

MOV DX,OFFSET NUM1

INT 21H

MOV AH,01H

INT 21H

MOV OP1,AL

;SECOND OPERAND

MOV AH,09H

MOV DX,OFFSET NUM2

INT 21H

MOV AH,01H

INT 21H

MOV OP2,AL

MOV AH,09H

MOV DX, OFFSET ANS

INT 21H

MOV AL,OP1

MOV BL,OP2

SUB AL,BL

AAS

OR AX, 3030H

; PRINT RESULT

MOV AH,0EH

INT 10H

;FOR CONTINUE

MOV AH,09H

MOV DX,OFFSET CONTINUE

INT 21H

MOV AH,01H

INT 21H

MOV CON,AL

MOV AL,CON

CMP AL,'Y'

JE START

CMP AL,'E'

JE EXIT

_MUL: ; PERFORMING MULTIPLICATION

MOV AH,09H

MOV DX,OFFSET MUL1

INT 21H

;FIRST OPERAND

MOV AH,09H

MOV DX,OFFSET NUM1

INT 21H

MOV AH,01H

INT 21H

SUB AL,30H

MOV OP1,AL

;SECOND OPERAND

MOV AH,09H

MOV DX,OFFSET NUM2

INT 21H

MOV AH,01H

INT 21H

SUB AL,30H

MOV OP2,AL

MOV AH,09H

MOV DX, OFFSET ANS

INT 21H

MOV AL,OP1

MOV BL,OP2

MUL BL

ADD AL,30H

; PRINT RESULT

MOV AH,0EH

INT 10H

;FOR CONTINUE

MOV AH,09H

MOV DX,OFFSET CONTINUE

INT 21H

MOV AH,01H

INT 21H

MOV CON,AL

MOV AL,CON

CMP AL,'Y'

JE START

CMP AL,'N'

JE EXIT _DIV: ; PERFORMING DIVISION

MOV AH,09H

MOV DX,OFFSET DIV1

INT 21H

;FIRST OPERAND

MOV AH,09H

MOV DX,OFFSET NUM1

INT 21H

MOV AH,01H

INT 21H

SUB AL,30H

MOV OP1,AL

;SECOND OPERAND

MOV AH,09H

MOV DX,OFFSET NUM2

INT 21H

MOV AH,01H

INT 21H

SUB AL,30H

MOV OP2,AL

MOV AH,09H

MOV DX, OFFSET ANS

INT 21H

MOV AX,0000H

MOV AL,OP1

MOV BL,OP2

DIV BL

ADD AL,30H

; PRINT RESULT

MOV AH,0EH

INT 10H

;FOR CONTINUE

MOV AH,09H

MOV DX,OFFSET CONTINUE

INT 21H

MOV AH,01H

INT 21H

MOV CON,AL

MOV AL,CON

CMP AL,'Y'

JE START

CMP AL,'E'

JE EXIT

EXIT: ; SAY GOOD BYE AND THEN EXIT

MOV AH,09H

MOV DX,OFFSET EX

INT 21H

.EXIT

END
