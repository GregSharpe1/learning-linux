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