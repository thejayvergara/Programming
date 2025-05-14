# BASH
## SPECIFY INTERPRETER
```bash
#!/bin/bash
```

## COMMAND SUBSTITUTION
```bash
echo -e $(echo "This is a command within a command\n")
```

## SPECIAL VARIABLES
```bash
# Number of arguments passed in
$#

# Argument by position
$1 $2 $3 $4

# List of arguments
$@

# Process ID
$$

# Exit Status
$?
```

## DECLARE VARIABLE
```bash
# Char, Int, String, Bool
localhost=127.0.0.1

# Arrays
names={jerry,john,joe)
echo ${names[2]}
```

## RANGE OF NUMBERS
```bash
# This is 1 to 100
{1..100}
```

## INTEGER OPERATORS
```bash
# Equal to
-eq

# Not equal to
-ne

# Less than
-lt

# Less than or equal to
-le

# Greater than
-gt

# Greater than or equal to
-ge
```

## STRING OPERATORS
```bash
# Equal to
==

# Not equal to
!=

# Less than in ASCII order
<

# Greater than in ASCII order
>

# String is empty
-z

# String is not empty
-n
```

## FILE OPERATORS
```bash
# File exist
-e

# File is a file
-f

# File is a directory
-d

# File is a symbolic link
-L

# File was modified after it was last read
-N

# Current user owns file
-O

# File group id matches current user
-G

# File size greater than 0
-s

# File has read permission
-r

# File has write permission
-w

# File has execute permission
-x
```

## LOGICAL OPERATORS
```bash
# Not
!

# And
&&

# Or
||
```

## ARITHMETIC OPERATORS
```bash
# Addition
+

# Subtraction
-

# Multiplication
*

# Division
/

# Modulus
%

# Increment
((variable++))

# Decerement
((variable--))
```

## IF-ELSE STATEMENT
```bash
if [[ -z $1]]
then
	echo -e "I do this\n"
elif [ condition ]
then
	echo -e "I do this instead\n"
else
	echo -e "Last choice\n"
fi
```

## CASE STATEMENT
```bash
case $input in
	"1") option_1 ;;
	"2") option_2 ;;
	"*") default_option ;;
esac
```

## FOR LOOP
```bash
for number in {1..100}
do
	echo $number
done
```

## WHILE LOOP
```bash
while [ true ]
do
	echo "Saying Hello World Forever!\n"
done
```

# STRING LENGTH
```bash
${#string}
```
