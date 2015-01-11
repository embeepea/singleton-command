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
tagging/identifying a specific process.
