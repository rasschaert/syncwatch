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
- sourcePath
- remotePath
- remoteHost

Check out syncwatch.sample.json for an example.

Don't forget to add a trailing slash to the source dir when necessary! Read rsync's man page if you don't know what I mean.

## Usage
```
kenny  laptop  ⋯  work  projectx  syncwatch
• Performing initial syncs
 ‣ [1] Syncing /home/kenny/work/projectx/code/ → devapp:/var/www/foo
 ‣ [2] Syncing /home/kenny/work/projectx/config/bar/ → devproxy:/etc/bar
• Watching for changes
 Ⅱ [0] Starting new watch on syncwatch.json
 Ⅱ [1] Starting new watch on /home/kenny/work/projectx/code/foo/
 Ⅱ [2] Starting new watch on /home/kenny/work/projectx/config/bar/
 ‣ [1] Syncing /home/kenny/work/projectx/code/foo/ → devapp:/var/www/foo
 ↻ [0] Configuration changed, stopping all watches and reloading
• Performing initial syncs
 ‣ [1] Syncing /home/kenny/work/projectx/code/foo/ → devapp:/var/www/foo
 ‣ [2] Syncing /home/kenny/work/projectx/config/bar/ → devproxy:/etc/bar
 ‣ [3] Syncing /home/kenny/work/projectx/code/qux/ → devapp:/var/www/qux
• Watching for changes
 Ⅱ [0] Starting new watch on syncwatch.json
 Ⅱ [1] Starting new watch on /home/kenny/work/projectx/code/foo/
 Ⅱ [2] Starting new watch on /home/kenny/work/projectx/config/bar/
 Ⅱ [3] Starting new watch on /home/kenny/work/projectx/code/qux/
 ‣ [3] Syncing /home/kenny/work/projectx/code/qux/ → devapp:/var/www/qux
^C
Syncwatch shutting down.
```

Kill with ^C when you're done.

## License
MIT
