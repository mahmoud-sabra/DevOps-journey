# Introduction to Shell Scripting

Learning shell scripting is a great way to automate tasks, manage files, and perform complex operations efficiently on Linux. Here’s a quick guide to get you started.

---

## Basics of Shell Scripting

### What is Shell Scripting?
Shell scripting is writing a series of commands for the shell (command line) to execute. Shell scripts are essentially batch files in Unix-based operating systems, written in languages like Bash, which is commonly used in Linux.

### Setting Up a Script File

1. **Create a file** with the `.sh` extension (e.g., `myscript.sh`).
2. Add a **shebang** (#!) at the top to specify the shell interpreter:
   ```bash
   #!/bin/bash
   ```

   
3. **Make the file executable** using the `chmod` command:
	```chmod +x myscript.sh ```

4. **Run the script** with `./myscript.sh`.
## First Script Example

```

#!/bin/bash
echo "Hello, World!"
```
##  Variables in Shell Scripting

You can define and use variables in shell scripts.
```
#!/bin/bash
name="Alice"
echo "Hello, $name"
```

## User Input

Shell scripts can also take user input.
```
#!/bin/bash
echo "Enter your name:"
read name
echo "Hello, $name!"

```

## Conditional Statements

Shell scripts support `if` statements for conditional logic.
```
#!/bin/bash
echo "Enter a number:"
read num
if [ $num -gt 10 ]; then
  echo "Number is greater than 10"
else
  echo "Number is 10 or less"
fi

```

## Loops

Loops allow repeated execution of commands.
**For Loop:**
```
#!/bin/bash
for i in 1 2 3 4 5; do
  echo "Number: $i"
done

```

**While Loop**:
```
#!/bin/bash
count=1
while [ $count -le 5 ]; do
  echo "Count: $count"
  ((count++))
done

```

## Functions

Functions help organize code into reusable blocks.
```
#!/bin/bash
greet() {
  echo "Hello, $1!"
}

greet "Alice"
greet "Bob"

```

## Script Arguments

You can pass arguments to a script from the command line.
```
#!/bin/bash
echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"

```
- `$0` is the script name.
- `$1`, `$2`, etc., represent command-line arguments.


