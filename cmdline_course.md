---
layout: default
---
# Command Line Tools for Linguists


**Overall Introduction**: This course offers a practical introduction to the UNIX command line environment, specifically designed for students in language and digital humanities fields. In today's rapidly evolving technology landscape, many linguistic tools and software rely on command-line interfaces, making it crucial for us to become familiar with this efficient way of interacting with our computers. 

In this course, we learned how to navigate the UNIX file system, use advanced tools to process corpus, process text files, run programs, and manage version control, gaining essential skills for language technology and computational research.
  
### Week 1: Introduction to the Command Line
In this week, we are taught how to set up the command line environment and learned some basic commands as well as terminal-based text editors(nano), some of the commands are listed in the following table:

| Commands   | Meaning                               |
|------------|---------------------------------------|
| ls         | list content of directory             |
| pwd        | print current working directory       |
| whoami     | determine the current username        |
| wget       | retrieve files from the internet      |
| mv         | move files or directory               |
| cat        | concatenate files to the standard output |
| less       | view file content, one page at a time |
| cp         | copy files or directory               |
| rm         | remove files and directory            |
| mkdir      | create a directory                    |
| cd         | change directory                      |


### Week 2: Navigating a UNIX System
This week, we explored UNIX file management, including how to copy, move, and delete directories. We also learned about system directories and how UNIX uses permissions to protect user privacy. Moreover, we would cover process management—how to control running programs—and finish with using `ssh` and `scp` to work on remote servers like CSC's puhti or taito.

While last week we studied how to manage files, this week we will focus on how to work with directories, most of the commands are similar, there are some additions:
+ **_cp -R_**: copy directory
+ **_rm -R_**: remove directory
+ **_rmdir_**: remove empty directory

More commands that are covered in this week include:
+ **_which_** is used to locate the executable file associated with a given command.
+ **_top_** displays current processes, real time monitoring.
+ **_fg_** is used to bring a background job to the foreground.
+ **_ps_** is used to view information about the processes running on your Linux system.
+ **_kill_** is used to terminate a process.

we also focused on connecting to remote servers and managing processes. We learned how to use SSH to securely connect to a server like CSC's Puhti. Once connected, we explored running commands on the server and managing processes. We also learned about the SCP command for securely copying files between your local computer and a remote server.

### Week 3: Introduction to Corpus Processing
This week, we explored text processing tools in UNIX, focusing on character encodings, which represent text in binary form. We also learned how to convert between different encodings and use key commands to search and manipulate text files, uncovering valuable linguistic information. In the second part, we dived into processing structured text files, such as tables, using UNIX commands designed to handle and organize structured data efficiently.

Firstly, in order to convert character encoding, the following commands are needed:
+ **_file_** can give us all kinds of useful information about a text file or other type of file like an image or a video.
+ **_iconv_** is an abbreviation of internationalization conversion which is used to convert text from one character encoding to another.
+ **_dos2unix_** converts the DOS text file format to UNIX format.

Then we studied how to generate a word list. For example, in order to create the word list of the text katinka rabe, the following steps can be used:
```
cat katinka_rabe.utf-8.txt | tr -s “[:space:][:punct:]” “\n” > katinka_rabe.utf-8.tok.txt
```
This command takes the content of the file katinka_rabe.utf-8.txt, replaces sequences of spaces and punctuation with a single newline, and writes the result to katinka_rabe.utf-8.tok.txt. Essentially, it tokenizes the text by splitting it into individual words or tokens, placing each on a new line.

```
sort katinka_rabe.utf-8.tok.txt > katinka_rabe.utf-8.tok.sort.txt
```
The sorts the contents of the file katinka_rabe.utf-8.tok.txt alphabetically and saves the sorted output to a new file named katinka_rabe.utf-8.tok.sort.txt.

```
uniq katinka_rabe.utf-8.tok.sort.txt > katinka_rabe.word_list.txt
```
Finally this command removes any consecutive duplicate lines from the sorted file katinka_rabe.utf-8.tok.sort.txt and saves the result into a new file called katinka_rabe.word_list.txt.

Moreover, **regular expressions** and **egrep** commands are shown in this week. For example, in order to search for noun phrases in Finnish that consist of adjectives and nouns in the inessive case, we can do the following:
```
egrep "\b[a-zåäö]*ss[aä] [a-zåäö]*ss[aä]\b" katinka_rabe.utf-8.txt
```
This command searches for lines where two consecutive words end with "ssa" or "ssä" and prints the matching lines from the file katinka_rabe.utf-8.txt. By applying this, we could extract noun phrases in the inessive case from the text.

### Week 4: Advanced Corpus Processing
This week, we expanded our understanding of UNIX text processing tools, focusing on more advanced techniques using command pipelines. This allowed us to combine simple commands into complex operations without generating numerous intermediate files. We also delved into the powerful sed command, which transforms text files by using regular expressions to find and replace patterns.

**_sed_** is a stream editor used for text manipulation, including substitution, insertion, and deletion. One example of using this command is the following:
```
sed '/^$/d' ulysses.txt > ulysses_noempty.txt
```
This command deletes empty lines (^$ matches empty lines) from ulysses.txt and saves the result in ulysses_noempty.txt.

Moreover we studied how to create frequency list, sentence per line format, and N-grams. I will demonstrate an example of creating frequency list and break down the code:
```
cat life_of_bee.txt | tr -s ‘\n\r\t ’ ‘\n’ | tr -dc “A-Za-z0-9\n’” | sort | uniq -c | sort -nr > life_of_bee.freq
```
The command will produce a file life_of_bee.freq containing a list of words from life_of_bee.txt, with their frequency counts sorted in descending order.

_tr -s '\n\r\t_: This part of the command collapses consecutive spaces, tabs, newlines, and carriage returns into a single newline, essentially breaking up the text into words.

_tr -dc 'A-Za-z0-9\n_: Removes all characters except letters (A-Za-z), numbers (0-9), and newlines (\n), which effectively cleans up the text by removing punctuation and special characters.

_uniq -c_: Counts the number of occurrences of each unique word.

_sort -nr_: Sorts the output in descending order by frequency (i.e., highest frequency words appear first).

### Week 5: Scripting and UNIX Configuration Files
This week's lesson focuses on creating bash scripts, which allow us to bundle together multiple UNIX commands into a single executable file. 
The summary of script creation process:
1. Create the script file using a text editor (e.g.: nano)
2. Add a shebang (#!/bin/bash)
3. Write the commands you want the script to execute.
4. Add command-line argument handling using $1, $2, etc.
5. Implement error checking with if statements for proper usage.
6. Make the script executable using chmod u+x.
7. Run the script directly by using ./script_name.sh.

Environment variables include:
- **_printenv_** displays the values of environment variables
- **_echo_** display a line of text
- **_export_** assign or remove environment variable

### Week 6: Installing and Running Programs
This week has been focused on gaining essential skills for managing software and development environments in Unix-like systems. I learned how to execute commands as the root user using sudo, which is crucial for system administration tasks. Installing software with package managers like apt-get on Linux and brew on macOS has also become second nature, as has installing Python packages via pip.

Some important commands for becoming the root user include:
+ **_su_**: switch user
+ **_sudo_**: become root user temporarily, for the duration of executing a single command
+ **_passwd_**: changes passwords for user accounts

We also studied how to install software including additional libraries and dependencies. One example of installing ImageMagick on macOS is shown below:
```
brew install imagemagick
```
**_locate_** is used to find file, using updated database

Moreover, we explored how to install python packages and python virtual environment. In order to install python we should run the following command on macOS:
```
brew install python3.7
```
- To check the version info upon startup, use _python_. 
- To install Python libraries using Python’s package manager, use _pip_.
- To install a package, use _pip install_.
- To create a virtual environemnt, use _venv_. 

### Week 7: Version Control
Moving into week 7, we focused on version control, which is crucial for managing changes in projects.
+ **_git_**: A widely used version control system that allows you to track changes in files and coordinate work on projects among multiple people.
+ **_GitHub_**: A platform that provides hosting for Git repositories, enabling collaboration and version control through a web interface.

Some basic git commands are listed in the following table
 

| Commands                 | Meaning                                               |
|--------------------------|-------------------------------------------------------|
| git init                 | Initializes a new Git repository                      |
| git clone <repository>   | Clones an existing repository to your local machine   |
| git add <file>           | Stages changes to be committed                        |
| git commit -m "message"  | Commits staged changes with a descriptive message     |
| git push                 | Pushes local changes to a remote repository           |
| git pull                 | Fetches and merges changes from a remote repository   |

One very useful tutorial is
<a href="http://www.youtube.com/watch?feature=player_embedded&v=HVsySz-h9r4" target="_blank">
    <img src="http://img.youtube.com/vi/HVsySz-h9r4/0.jpg" 
    alt="Version Control with Git and GitHub" width="240" height="180" border="10" />
</a>

### Week 8: Jekyll and Gihub Pages
- **GitHub Pages** is a static site hosting service that allows us to host a website about ourselves, our organization, or our project directly from a repository on GitHub. 
- **Jekyll** is a simple, blog-aware, static site generator perfect for personal, project, or organization sites.

Here is the step of clone a Jekyll template:
1. Create a template directory
```
mkdir templates
```
2. Change into the templates directory
```
cd templates
```
3. Clone a template repository
```
git clone https://github.com/handecelikkanat/cayman.git
```
4. Change into the cloned directory
```
cd cayman
```
5. Install dependencies
```
bundle install
```
6. Build and serve the site
```
bundle exec jekyll serve
``` 

That's all!!:
![alt text]( https://github.blog/wp-content/uploads/2021/11/nat-social.png?resize=1200%2C630 "Logo Title Text 1")
