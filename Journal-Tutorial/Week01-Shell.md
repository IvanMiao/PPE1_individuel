# Week 01 - Shell

[TOC]

## 1. Basic commands

0. **Syntax**:
   
    `Command [-Options] Argument`
    
    <u>**Attention**</u>: In Shell, spaces act as separators. This can cause troubles when working with file paths that contain spaces. For a solution, see: [How To Deal With Spaces in Paths](https://medium.com/@leedowthwaite/dealing-with-spaces-in-paths-f26856aef06f) 

<br/>

1. **Don't get lost in your files**

When navigating through your directories, it’s important to know where you are and what files are around you. For example, If we use `pwd` to print the path, we might see something like that: `/home/username/Documents` , which tells us that we are in the directory `Documents`. This helps us understand our position, allowing us to move forward or move back on this path.

| **Command** |         **Options**          |      **Full Name**      |                     **Function**                     |
| :---------: | :--------------------------: | :---------------------: | :--------------------------------------------------: |
|    `pwd`    |                              | print working directory |           show the current directory path            |
|    `ls`     | `-l` (detailed) , `-a` (all) |          list           | list all files and directories in the current folder |
|    `cd`     |                              |    change directory     |            move to a different directory             |

​	When using `cd` ,  `./` refers to the current directory, while `../` takes us to the parent directory. `/` represents the root directory, and `~/` refers to user's home directory.

<br/>

2. **Managing files and directories**

   To create new files or organize files into different folders:

| **Command** |        **Option**s        | **Full Name**  |                   **Function**                    |
| :---------: | :-----------------------: | :------------: | :-----------------------------------------------: |
|   `mkdir`   |                           | make directory |              create a new directory               |
|   `touch`   |                           |       -        |               create an empty file                |
|    `rm`     | `-r` : delete a directory |     remove     |          delete a file ***permanently***          |
|    `mv`     |                           |      move      | move or rename a file/directory to a new location |
|    `cp`     |                           |      copy      |           copy a file to a destination            |

<br/>

3. **Viewing file contents**
   
   We can display file contents on the terminal, without opening any editors!

| **Command** | **Option**s | **Full Name** |                    **Function**                    |
| :---------: | :---------: | :-----------: | :------------------------------------------------: |
|    `cat`    |             |  concatenate  |     display the content of a file all at once      |
|   `less`    |             |       -       | open the file for viewing, allow scrolling through |
|   `head`    |             |       -       |       print the first 10 lines of each file        |
|   `tail`    |             |       -       |        print the last 10 lines of each file        |

<br/>

4. **Other**

| **Command** | **Option**s |          **Full Name**          |                    **Function**                    |
| :---------: | :---------: | :-----------------------------: | :------------------------------------------------: |
|    `man`    |             |             manual              | displays the manual for a given command. **RTFM!** |
|   `echo`    |             |                -                |       print a line of text or variable value       |
|   `grep`    |             | global regular expression print |  search for a specific text pattern within a file  |

<br/>

### Wildcards

Wildcard (**fr**: caractères de remplacement; **zh**: 通配符)

> In computer (software) technology, a wildcard is a symbol used to replace or represent zero or more characters. 
>
> ——Wikipedia

When specifying file names/paths:

- the question mark `?` matches exactly one character. 

- the asterisk character `*` matches zero or more characters.

---

## 2. Shell Script

- Some Tutorials:
  
  - [The Shell Scripting Tutorial](https://www.shellscript.sh/) (EN)
  
  - [Scripts Shell](https://linux.goffinet.org/administration/scripts-shell/) [FR]
  
  - [Shell编程](https://shellscript.readthedocs.io/zh-cn/latest/index.html) [ZH]
  
  - [学习如何编写 Shell 脚本（基础篇）](https://juejin.cn/post/6930013333454061575) [ZH]



### Basic Grammar

- an example:

```bash
#!/bin/sh

for month in {01..12}; do
	mkdir -p "$month"
	mv 2016_"$month"* "$month"/
done
```

**Line-by-line Breakdown:**

1.  `for month in {01..12};do`

   - This line starts a loop that will repeat for each month of the year, from `01` to `12`. The `{01..12}` syntax means that the loop will iterate with the values `01`, `02`, `03`, and so on, up to `12`.

   - For each iteration, the variable `month` will take one of these values.

2.  `mkdir -p "$month"`

   - This command creates a directory named after the current value of `month`. The dollar `$` means `month` is a variable. For example, when `month` is `01`, it creates a directory called `01`.

   - The `-p` option ensures that no error is raised if the directory already exists.

3.  `mv 2016_"$month"* "$month"/`

   - The `mv` command moves files into the corresponding directory. It moves all files that start with `2016_` followed by the value of `month`. The `*` is a wildcard that matches any characters after `2016_"$month"` (e.g. it could match `2016_01_report.txt` or `2016_01_data.csv`).

   - Finally, the `"$month"/` indicates the target directory where the files should be moved (e.g. the `01/` directory).

4.  `done`

   - This closed the loop, meaning the script will go back to the beginning, increment the `month` variable to the next value, and repeat the process for the next month.



### 	Rewrite a script in one line

​	If we do that, a script becomes a command that can be run directly in the terminal. (Hope it's not too long)

​	Rewrite the script above:
``` bash
for month in {01..12};do mkdir -p "$month";mv 2016_"$month"* "$month"/;done
```

