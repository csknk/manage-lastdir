# Save the Current Working Directory

Save the current working directory into a logfile. Easily change into to the last saved directory in the log.

Why?
----
You're working late, on a project that is nested 5 or 6 directories deep and you decide to stop work. You get up the next day and can't remember where your project is located, so you waste 5 minutes running `find` to track it down. You can either:

* Jot down the path on a piece of paper before shutting down or...
* Run `lastdir` when you finish work and `lastdir -o` to restart where you left off.

Usage
-----
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
Notes
-----
The "open" option (`-o`) uses:

```bash
cd $(tail -1 ${LASTDIR_LOG} | head -1)
```
It would be simpler to use something like:

```bash
cd $(awk 'END{print}' ${LASTDIR_LOG})

# or
cd $(sed -n '$p' ${LASTDIR_LOG})
```
It might be nice to be able to select a path based on an index from the last line in the log file.

### Make OPTIND local
Note that because the script is sourced rather than run, you need to make sure `${OPTIND}` is local to the function - otherwise, there will be unexpected behaviour when invoking multiple times.   
