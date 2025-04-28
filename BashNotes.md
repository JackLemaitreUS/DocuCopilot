#!/bin/bash
```sh  
# Bash 5 Full Cheat Sheet

# 1. Loops

## For Loop
for i in {1..5}; do
    echo "Iteration $i"
done

## While Loop
counter=1
while [ $counter -le 5 ]; do
    echo "Counter: $counter"
    ((counter++))
done

## Until Loop
counter=1
until [ $counter -gt 5 ]; do
    echo "Counter: $counter"
    ((counter++))
done

# 2. Conditional Statements

## If Statement
var=10
if [ $var -gt 5 ]; then
    echo "Var is greater than 5"
elif [ $var -eq 5 ]; then
    echo "Var is exactly 5"
else
    echo "Var is less than 5"
fi

## Case Statement
read -p "Enter a fruit: " fruit
case $fruit in
    apple) echo "You chose Apple";;
    banana) echo "You chose Banana";;
    *) echo "Unknown fruit";;
esac

# 3. User Input

## Reading Input
read -p "Enter your name: " name
echo "Hello, $name!"

## Reading Input Without Echoing (for passwords)
read -s -p "Enter password: " password
echo -e "\nPassword saved securely."

# 4. Functions

## Defining a Function
function greet() {
    echo "Hello, $1!"
}

## Calling a Function
greet "User"

## Returning Values
function add_numbers() {
    echo "$(($1 + $2))"
}

result=$(add_numbers 5 3)
echo "Sum: $result"

## Local Variables
function display_message() {
    local message="This is a local variable"
    echo "$message"
}

display_message

## Function Arguments
function sum_all() {
    local total=0
    for num in "$@"; do
        total=$((total + num))
    done
    echo "Total sum: $total"
}

sum_all 3 5 7 2

## Error Handling in Functions
function safe_operation() {
    set -e
    mkdir test_directory
    cd test_directory
}

safe_operation

## Recursive Function
function countdown() {
    if [ "$1" -gt 0 ]; then
        echo "$1"
        countdown $(($1 - 1))
    fi
}

countdown 5

# 5. Arrays

## Declaring an Array
fruits=("apple" "banana" "cherry")

## Accessing Elements
echo "First fruit: ${fruits[0]}"
echo "All fruits: ${fruits[@]}"

# 6. Associative Arrays

declare -A colors
colors[red]="#FF0000"
colors[blue]="#0000FF"
echo "Red color code: ${colors[red]}"

# 7. Arithmetic Operations

num1=10
num2=5
echo "Sum: $((num1 + num2))"
echo "Product: $((num1 * num2))"
echo "Exponentiation: $((num1 ** num2))"

# 8. String Operations

str="Bash Scripting"
echo "Length: ${#str}"
echo "Substring: ${str:0:4}"  # "Bash"

# 9. Error Handling

set -e   # Exit script on error
set -u   # Treat undefined variables as errors
set -o pipefail # Fail on pipeline errors

# 10. Mapfile (readarray)

mapfile -t lines < file.txt
echo "${lines[0]}"  # Prints the first line from file.txt

# 11. Process Substitution

diff <(ls dir1) <(ls dir2)

# 12. Extended Globbing

shopt -s extglob
ls !(*.txt)  # Lists all files except .txt

# 13. Nameref Variables

declare -n ref_var=name
name="Bash"
echo "$ref_var" # Prints "Bash"

```
