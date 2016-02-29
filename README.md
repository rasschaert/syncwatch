# Syncwatch
Syncs local folders to one or more remote machines when a change on the filesystem occurs.

Syncwatch uses the awesome cross-platform [fswatch](https://github.com/emcrisostomo/fswatch) to watch for filesystem changes, and rsync to propagate these changes.

Many other (editor built-in) alternatives use language libraries for SCP or SFTP which often ignore your SSH configuration. This script simply shells out to regular rsync, so you get the advantage of your ~/.ssh/config being used.

Rsync is called with the --delete option in order to clean up obscolete files. Doublecheck your paths so you don't accidentally delete something on your remote host!

## Installation
Just make the script executable and put it a folder in your $PATH.

## Dependencies:
- ruby
- [fswatch](https://github.com/emcrisostomo/fswatch)
- rsync

## Configuration
Add one or more sets of the following to the syncwatch.json configuration file:
- sourcedir
- remotedir
- remotehost

See syncwatch.sample.json for an example.

Don't forget to add a trailing slash to the source dir when necessary! Read rsync's man page if you don't know what I mean.

## Usage
```
[kenny@laptop development]$ ls
foo
bar
syncwatch.json

[kenny@laptop development]$ syncwatch
Starting new watch [0] on /home/kenny/development/foo/css/
Starting new watch [1] on /home/kenny/development/bar/webserver-config/
  [1] Syncing /home/kenny/development/bar/webserver-config/proxy.conf to devbox-02:/etc/httpd/conf.d
```

Kill with ^C when you're done.

## License
MIT
