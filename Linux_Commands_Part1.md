
# Linux Commands from Basic to Advanced

---

### **Beginner Level**

1. `ls`  
   ```bash
   ls
   ```
   Lists files and directories in the current directory.

2. `pwd`  
   ```bash
   pwd
   ```
   Prints the current directory path.

3. `cd`  
   ```bash
   cd /path/to/directory
   ```
   Changes the directory to the specified path.

4. `mkdir`  
   ```bash
   mkdir new_folder
   ```
   Creates a new directory named "new_folder".

5. `rmdir`  
   ```bash
   rmdir empty_folder
   ```
   Removes an empty directory named "empty_folder".

6. `touch`  
   ```bash
   touch file.txt
   ```
   Creates a blank file named "file.txt".

7. `rm`  
   ```bash
   rm file.txt
   ```
   Deletes "file.txt". Add `-r` for directories: `rm -r folder`.

8. `cp`  
   ```bash
   cp file1.txt file2.txt
   ```
   Copies `file1.txt` to `file2.txt`.

9. `mv`  
   ```bash
   mv oldname.txt newname.txt
   ```
   Renames or moves a file.

10. `cat`  
    ```bash
    cat file.txt
    ```
    Displays the contents of "file.txt".

11. `more`  
    ```bash
    more file.txt
    ```
    Views "file.txt" one page at a time.

12. `less`  
    ```bash
    less file.txt
    ```
    Like `more` but with more navigation options.

13. `head`  
    ```bash
    head -n 5 file.txt
    ```
    Shows the first 5 lines of "file.txt".

14. `tail`  
    ```bash
    tail -n 5 file.txt
    ```
    Shows the last 5 lines of "file.txt".

15. `echo`  
    ```bash
    echo "Hello, World!"
    ```
    Prints "Hello, World!" to the terminal.

16. `clear`  
    ```bash
    clear
    ```
    Clears the terminal screen.

17. `which`  
    ```bash
    which bash
    ```
    Shows the path of the `bash` executable.

18. `find`  
    ```bash
    find /home -name file.txt
    ```
    Searches for "file.txt" in the `/home` directory.

19. `locate`  
    ```bash
    locate file.txt
    ```
    Finds the location of "file.txt" (requires `locate` database update).

20. `du`  
    ```bash
    du -sh /path/to/folder
    ```
    Displays the size of a directory.

21. `df`  
    ```bash
    df -h
    ```
    Shows disk space usage in a human-readable format.
