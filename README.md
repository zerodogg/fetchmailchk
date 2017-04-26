# fetchmailchk - a fetchmail monitoring tool

`fetchmailchk` will check if fetchmail is working. It does this by reading from
journald and checking when fetchmail last retrieved something.

fetchmailchk thus makes some demands on how fetchmail is configured:

- The system must be using journald as its syslog facility
- fetchmail must be configured to log to syslog
- fetchmailchk must be run as the same user as fetchmail

## Usage

fetchmailchk is just a monitoring tool. It will tell you if fetchmail is
working or not. It is then up to you to restart the fetchmail instance if you
need to. Here's an example of how that could be done with a shell script:

    #!/bin/bash
    if ! fetchmailchk --pidfile=~/.fetchmail.pid; then
        fetchmail --quit
        fetchmail -d 600
    fi
