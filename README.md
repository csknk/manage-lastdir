# Save the Current Working Directory

Save the current working directory into a logfile. Change to the last saved directory in the log.

Options:
* No options: save the output of $PWD to the log
* `-o`: Open the last location saved in the log
* `-p`: Print the log
* `-d`: Delete all log entries except for the last line

Because the functionality involves opening the shell in a specified directory, this file
should be sourced rather than run.

To do this, save the current file in your `$PATH` and create an alias such as:
```bash
# ~/.bashrc or similar
alias lastdir=". lastdir"
```
