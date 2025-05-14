# BASH
## SPECIFY INTERPRETER
```bash
#!/bin/bash
```

## COMMAND SUBSTITUTION
```bash
echo -e $(echo "This is a command within a command\n")
```

## PREDEFINED VARIABLES
```bash
# Number of arguments passed in
$#

# Argument by position
$1 $2 $3 $4
```

## DECLARE VARIABLE
```bash
localhost=127.0.0.1
```

## INCREMENT AND DECREMENT VARIABLE
```bash
((variable++))
((variable--))
```	

## RANGE OF NUMBERS
```bash
# This is 1 to 100
{1..100}
```

## COMPARISON OPERATORS
```bash
# Equal to
-eq

# Less than
-lt

# Greater than
-gt
```

## IF-ELSE STATEMENT
```bash
if [ true ]
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
