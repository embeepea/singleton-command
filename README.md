singleton-command
=================

This is a little unix/linux command line utility to facilitate executing a task
in a situation where you want to make sure that no other copy of that task is
already running.

usage
-----

    singleton-command KEY COMMAND

This checks the list of currently running processes for a process,
other than the current one, whose argument list contains KEY.  If no
such process is found, runs COMMAND in a subshell and exits with its
exit status.  If a process other than the current one is found with
KEY in its argument list, exits immediately with no error.

KEY can be any string and simply serves as a general way of
tagging/identifying processes.

Conceptually, this is a low-tech kind of locking mechanism.  Note
that this technique is not as robust as
a real locking mechanism.  In particular, be mindful
of situations where the `singleton-command` command may get
repeated in a subshell.  In particular, if you put something
like

    singleton-command foo-id-123 ./foo
    
in a crontab file for running as a cron job, the cron
system will execute the command

    sh -c 'singleton-command foo-id-123 ./foo'
    
which in turn runs

    singleton-command foo-id-123 ./foo
    
in a subshell, thus creating two processes containing the key
`foo-id-123`, which will prevent `singleton-command` from
excuting `./foo`.

This limitation can be worked around by using a wrapper script that
runs the `singleton-command` command, and having the cron entry reference
the wrapper script.
