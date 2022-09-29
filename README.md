# piwatch
Watch for new RasPiOS release and notify

piwatch is a simple script to check for a RasPiOS release newer than the one you're already aware of.

If a new release is available, piwatch can send email or log to the system log. If you want to use piwatch in your own script, piwatch exits with success (0) if there is a new RasPiOS release.

## piwatch command

   `piwatch [switches]`

### Command-line switches

All switches are optional, but affect the app behavior.

* `--date` *yyyy-mm-dd* &mdash; Check for new editions after given date. If not specified, date in /usr/local/etc/piwatch is used. If --date is specified, /usr/local/etc/piwatch will not be updated unless --update
* ` --edition` *name* &mdash; Name of edition to check
    * Valid edition names: raspios_armhf, raspios_arm64, raspios_lite_armhf, raspios_lite_arm64, raspios_full_armhf, raspio_full_arm64
    * If `--edition` is not specified, the default is *raspios_arm64*
* `--mailfrom` *email-from-address* &mdash; Where the mail should come from
    * Format: either mailaddr\@domain.com or \"firstname lastname\<person\@somewhere.com\>\"
* `--mailto` *email-to-address* &mdash; What email address to send to. See *Sending mail* below.
* `--logger` &mdash; Log to the system log if there is an update
* `--update` &mdash; Update /usr/local/etc/piwatch even if --date was specified. This can be used to correctly reset the contents of /usr/local/etc/piwatch
* `--verbose` &mdash; Print a tiny bit of extra goop on the console

## Sending mail

In order for piwatch to send mail, both `--mailfrom` and `--mailto` must be specified. piwatch does no syntax or validity checking on these switch values.

piwatch uses the `mail` command to send mail. piwatch was tested using the bsd-mailx command from package bsd-mailx. When installed, it is symlinked to /bin/mail.

Other mail commands should work, but may require changing the piwatch code.

In addition to the mail command, you need to have a mail sender, such as postfix or exim. There are guides on the internet for this. Alternatively, you can change the piwatch code to use a different mailer if you know a bit of python.

## Scheduling piwatch

Schedule piwatch to run daily with cron.

## Important note

piwatch does not need to be run with sudo. HOWEVER, if you decide to run it without sudo, you must:
```
sudo touch /usr/local/etc/piwatch
sudo chown myuser.users /usr/local/etc/piwatch
```
Where *myuser* is the username under which you run piwatch.
