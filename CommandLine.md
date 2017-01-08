#Command Line


**ls** <br/>
*lists files and folders in the direction you are*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**ls -a**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*shows also hidden files*
<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**ls -l**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*lists all files and directories as a table (access rights, number of hard links, file owner, groupname, size, date & time, name)*
<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**ls -t**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*orders the files & directories by the time they were last modified*

**pwd**<br/>
*prints the directory you are in*

**cd**<br/>
*changes directory*: cd myfolder/mysubfolder, cd .., cd ../anotherfolder, etc...

**mkdir**<br/>
*makes a new directory(new folder)*

**touch**<br/>
*creates a new file*

**cp**<br/>
*copies files & directories into file or directory (last argument is the destination)*<br/>
 &nbsp;&nbsp;&nbsp;&nbsp;<strong> cp \* </strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*use wildcard to select all files in a directory (or all files starting with a m: m* *)
<br/>

**mv**<br/>
*moves files & directories into directory (last argument is the destination) or renames a file*<br/>
 &nbsp;&nbsp;&nbsp;&nbsp;<strong> mv somefile.txt somenewname.txt </strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*moving a file into a file rename it*
<br/>

**rm**<br/>
*removes files & directories*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**rm -r**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*removes recursively all files and folder contained*
<br/>

**echo** <br/>
*echoes the string back to the terminal as standard output*<br/>
&nbsp;&nbsp;&nbsp;&nbsp; *stdin: information inputted into the terminal through the keyboard or input device<br/>*
&nbsp;&nbsp;&nbsp;&nbsp; *stdout: information outputted after a process is run<br/>*
&nbsp;&nbsp;&nbsp;&nbsp; *stderr: error message outputted by a failed process<br/>*
&nbsp;&nbsp;&nbsp;&nbsp;*(Redirection reroutes standard input, standard output, and standard error to or from a different location)*
<br/>

**cat**<br/>
*outputs the content of a file to the terminal*

**less**<br/>
*similar to cat but displays text one page at a time*

**>**<br/>
*redirects the standard output (left) to a file (right)*

**>>**<br/>
*takes the standard output (left) and appends it to a file (right)*

**<**<br/>
*redirects the standard input from the file (right) and inputs it into the program (left)*

**|**<br/>
*take the standard output of the command on the left and pipes it as standard input into the command on the right (command to command redirection)*

**wc**<br/>
*output the numbers of lines, words, characters*

**sort**<br/>
*takes the standard input and orders it alphabetically for the standard output*

**uniq**<br/>
*filters out <strong>adjacent</strong>, duplicate lines in a file*<br/>
*(A more effective way to call uniq is to call sort to alphabetize a file, and "pipe" the standard output to uniq)*<br/>

**grep**<br/>
*"global regular expression print", searches files (last arg) for lines that match a pattern and returns the results*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**grep -i**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*ignore case*
<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**grep -R**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*searches all files in a directory and outputs filenames and lines containing matched results (Recursive)*
<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**grep -Rl**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*searches all files in a directory and outputs only filenames with matched results*
<br/>

**sed**<br/>
*"stream editor", accepts standard input and modifies it based on an expression, before displaying it as output data*<br/>
*⇒ similar to find and replace*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;→ sed 's/snow/rain/g' myfile.txt <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *- s: substitution, <strong>always</strong> used when using sed for substitution<br/>*
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *- snow: search string (text to find)<br/>*
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *- rain: replacement string (text to add in place)<br/>*
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *- g: "global", will replace <strong>all</strong> instances of the search string(without 'g' it replaces only the first instance)<br/>*
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *- myfile.txt: the file to look into<br/>*

**clear** <br/>
*clear the terminal*<br/>

**echo $HOME**<br/>
*displays the path of the home directory*<br/>

**echo $PATH**<br/>
*the PATH variable lists which directories contain scripts*<br/>

**env**<br/>
*returns a list of the environment variables for the current user*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**env | grep PATH**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*displays the value of a single environment variable (here PATH)*
<br/>

**which** <br/>
*Shows the path of the service/command*<br/>

**sudo apt-get --purge remove<br/>**
*Remove a package and its config files<br/>*
--------------------------------------------------------
~/.bash\_profile : file used to store environment settings <br/>
&nbsp;&nbsp;&nbsp;&nbsp;*use <strong>source ~/.bash_profile</strong> to activates the changes without having to restart a new session*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*<strong>alias</strong>: command allows you to create keyboard shortcuts*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*alias pd="pwd" creates the alias pd for the pwd command (no space around =)*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*<strong>export</strong>:  sets and exports an environment variable*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*export USER="Jane Doe" sets the environment variable USER to a name "Jane Doe"*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*export PS1=">> " changes the style of the command prompt*<br/>
