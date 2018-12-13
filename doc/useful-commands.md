# *Kicking* users from SSH session

## Using a combination of `skill` and `who` to kill an SSH session for the given user.

### Commands

* `$ who` - locate the user you wish to terminate SSH session

        deploy   pts/0        2018-12-13 11:37 (192.168.0.256)
        greg     pts/1        2018-12-13 11:29 (192.168.0.256)

* `$ sudo skill -KILL -u deploy`

        Connection to 192.168.0.202 closed.

### Extra credit write to the users' SSH session

* `$ echo "system message: About to shutdown system" | write deploy pts/0`

        Message from greg@jenkins on pts/1 at 11:42 ...
        System about to shutdown
        EOF

## Using fgrep, awk, sed and xargs

### I was attempting to cover all previously learnt knowledge from LFCE exam with this command (plus use of `xargs`). The following command was used to open a yml file in vim file that contained the string "import database" (some stripping through the use of sed was required)

* `$ fgrep -rni "import database" . | awk '/main.yml/{print $1}' | sed 's/:.*//' | xargs vim` 

        fgrep is used to find a string within a the current directory
        `-r` arguement is used to search recursive throughout this current directory
        `-i` argument is to ignore case when searching
        `-n` argument is used to output the line number (didn't end up needing that one)

        awk (explained within basic-commands.md) is used to print the first instance from fgrep search

        sed (explained within basic-commands.md) is used to strip everything after the ':' as that wouldn't be a valid path

        xargs is used to pass the path into vim in this case.