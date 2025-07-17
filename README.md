# linux-shell-scripting-project


# Bash Script for Generating a Multiplication Table

## Project Objective
The goal of this project was to create a Bash script that generates a multiplication table for a number entered by the user. The user can choose to display either a full multiplication table (1 to 10) or a partial table within a specified range. The script also allows the user to choose the order of the table: ascending or descending.

---

##  How I Did the Project

### 1. Prompt User Input
I began the script by using `read` to ask the user to enter a number. This number is the base for the multiplication table.

```
read -p "Enter a number for the multiplication table: " number
```

### 2. Table Type Selection
Next, I prompted the user to choose between a full or partial table by entering `f` or `p`.

```
read -p "Do you want a full table or a partial table? (Enter 'f' for full, 'p' for partial): " choice
```

### 3. Ask for Output Order
I then asked the user to choose the output order (ascending or descending):

```
read -p "Do you want the table in ascending or descending order? (Enter 'a' or 'd'): " order
```

### 4. Full Table Logic
If the user selected a full table, I used a **list-form `for` loop**:

```bash
# Ascending
for i in {1..10}; do
  echo "$number x $i = $((number * i))"
done

# Descending
for i in {10..1}; do
  echo "$number x $i = $((number * i))"
done
```

### 5. Partial Table Logic
If the user selected a partial table, I used a **C-style `for` loop** to dynamically loop through a specified range:

```
# Ascending
for (( i=start; i<=end; i++ )); do
  echo "$number x $i = $((number * i))"
done

# Descending
for (( i=end; i>=start; i-- )); do
  echo "$number x $i = $((number * i))"
done
```

### 6. Input Validation
If the user inputs invalid options or range values, the script falls back to default behavior and prints a full table in ascending order.

---

## What I Learned

- How to use `read` to accept user input
- The difference between **list-form** and **C-style** `for` loops
- How to use conditional statements (`if`, `elif`, `else`)
- How to validate input and handle edge cases
- How to use nested conditionals for user choices
- How to enhance Bash script interactivity

---

## Bonus Feature

I added a loop that allows the user to **run the program repeatedly** without restarting:

```
while true; do
  ...
  read -p "Do you want to run the program again? (y/n): " repeat
  if [ "$repeat" != "y" ]; then
    echo "Goodbye!"
    break
  fi
done
```

---

Complete Script With Comments:

```
#!/bin/bash

# Loop to allow repeat usage
while true; do
  read -p "Enter a number for the multiplication table: " number
  read -p "Do you want a full table or a partial table? (Enter 'f' for full, 'p' for partial): " choice
  read -p "Do you want the table in ascending or descending order? (Enter 'a' or 'd'): " order

  if [ "$choice" == "f" ]; then
    echo "Full multiplication table for $number:"

    if [ "$order" == "a" ]; then
      # List-form loop: ascending
      for i in {1..10}; do
        echo "$number x $i = $((number * i))"
      done
    elif [ "$order" == "d" ]; then
      # List-form loop: descending
      for i in {10..1}; do
        echo "$number x $i = $((number * i))"
      done
    else
      echo "Invalid order. Showing ascending order by default:"
      for i in {1..10}; do
        echo "$number x $i = $((number * i))"
      done
    fi

  elif [ "$choice" == "p" ]; then
    read -p "Enter the starting number (1–10): " start
    read -p "Enter the ending number (1–10): " end

    if [ "$start" -le "$end" ]; then
      echo "Partial multiplication table for $number from $start to $end:"

      if [ "$order" == "a" ]; then
        # C-style loop: ascending
        for (( i=start; i<=end; i++ )); do
          echo "$number x $i = $((number * i))"
        done
      elif [ "$order" == "d" ]; then
        # C-style loop: descending
        for (( i=end; i>=start; i-- )); do
          echo "$number x $i = $((number * i))"
        done
      else
        echo "Invalid order. Showing ascending order by default:"
        for (( i=start; i<=end; i++ )); do
          echo "$number x $i = $((number * i))"
        done
      fi
    else
      echo "Invalid range. Showing full table instead:"
      for i in {1..10}; do
        echo "$number x $i = $((number * i))"
      done
    fi

  else
    echo "Invalid choice! Please enter 'f' or 'p'"
  fi

  read -p "Do you want to run the program again? (y/n): " repeat
  if [ "$repeat" != "y" ]; then
    echo "Goodbye!"
    break
  fi
done
```

## Final Thoughts

This project helped me gain deeper understanding of Bash scripting by combining loops, conditionals, user inputs, and custom output formatting into a clean, interactive program.
