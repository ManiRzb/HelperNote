
# Rsync

`rsync` is a powerful utility for efficiently transferring and synchronizing files across local drives, networks, and remote servers. It offers a wide range of options for various use cases.

## Options

Here are some of the most commonly used `rsync` options:

- `-a, --archive`: Archive mode; equals `-rlptgoD` (no `-H,-A,-X`)
- `-v, --verbose`: Increase verbosity
- `-q, --quiet`: Suppress non-error messages
- `-z, --compress`: Compress file data during the transfer
- `-r, --recursive`: Recurse into directories
- `-u, --update`: Skip files that are newer on the receiver
- `--delete`: Delete extraneous files from destination directories
- `--exclude=PATTERN`: Exclude files matching PATTERN
- `--exclude-from=FILE`: Read exclude patterns from FILE
- `--include=PATTERN`: Include files matching PATTERN
- `--include-from=FILE`: Read include patterns from FILE
- `-e, --rsh=COMMAND`: Specify the remote shell to use
- `--progress`: Show progress during transfer
- `-h, --human-readable`: Output numbers in a human-readable format
- `--dry-run`: Perform a trial run with no changes made
- `-P`: Equivalent to `--partial --progress`
- `--partial`: Keep partially transferred files
- `--bwlimit=RATE`: Limit socket I/O bandwidth
- `--chmod=CHMOD`: Affect file and/or directory permissions
- `-l, --links`: Copy symlinks as symlinks
- `-L, --copy-links`: Transform symlink into referent file/dir
- `--copy-unsafe-links`: Copy links outside the source tree
- `--safe-links`: Ignore links outside the destination tree
- `-H, --hard-links`: Preserve hard links
- `-p, --perms`: Preserve permissions
- `-E, --executability`: Preserve the executability
- `--chmod=CHMOD`: Change file and directory permissions
- `-t, --times`: Preserve modification times
- `-O, --omit-dir-times`: Omit directories when preserving times
- `--super`: Receiver attempts super-user activities
- `--fake-super`: Store/retrieve privileged attrs using xattrs
- `-S, --sparse`: Handle sparse files efficiently
- `--preallocate`: Preallocate space on file system pre-transfer
- `--compress-level=NUM`: Explicitly set compression level
- `--skip-compress=LIST`: Skip compressing files with suffix in LIST
- `-C, --cvs-exclude`: Auto-ignore files the same way CVS does
- `-T, --temp-dir=DIR`: Create temporary files in directory DIR
- `--compare-dest=DIR`: Compare destination files for backup
- `--backup`: Make backups (see `--suffix` & `--backup-dir`)
- `--backup-dir=DIR`: Make backups into hierarchy based in DIR
- `--suffix=SUFFIX`: Set backup suffix (default ~ unless overridden)
- `--link-dest=DIR`: Hardlink to files in DIR when unchanged
- `-I, --ignore-times`: Don't skip files that match in size
- `--size-only`: Skip files that match in size
- `--modify-window=NUM`: Timestamp window (seconds) for file match
- `--daemon`: Run as an rsync daemon
- `--password-file=FILE`: Read daemon-access password from FILE
- `--list-only`: List the files instead of copying them
- `--bwlimit=KBPS`: Bandwidth limit (KBytes per second)
- `--write-batch=FILE`: Write a batched update to FILE
- `--only-write-batch=FILE`: Like --write-batch but w/o updating destination
- `--read-batch=FILE`: Read a batched update from FILE
- `--protocol=NUM`: Force an older protocol version to be used
- `-4, --ipv4`: Prefer IPv4
- `-6, --ipv6`: Prefer IPv6
- `--version`: Print version number
- `(-h) --help`: Show this help message

_Note: This list includes the most commonly used options, but `rsync` has even more options for specialized use cases. Always refer to the `rsync` man page (`man rsync`) for the most comprehensive and detailed information._

## Example Commands

### Basic File Transfer
```bash
rsync -av /path/to/source /path/to/destination
```
Synchronizes files from the source directory to the destination directory, preserving permissions and timestamps, with verbose output.

### Remote File Transfer

 Over SSH
```bash
rsync -avz /local/dir user@remote_host:/remote/dir
```
Transfers files from a local directory to a remote directory over SSH, with data compression.

### Dry Run (Simulation)
```bash
rsync -avz --dry-run /source/dir /destination/dir
```
Simulates the transfer process without making any actual changes, useful for testing.

### File Transfer with Deletion
```bash
rsync -av --delete /source/dir /backup/dir
```
Synchronizes the source to the destination directory, deleting files in the destination that are not present in the source.

### Exclude Files
```bash
rsync -av --exclude 'pattern' /source/dir /destination/dir
```
Transfers files while excluding those that match a specified pattern.

### Incremental Backup
```bash
rsync -av --link-dest=/path/to/previous/backup /source/dir /path/to/backup
```
Creates an incremental backup, hard-linking unchanged files to a previous backup for efficiency.

### Transferring a Single File
```bash
rsync -av /path/to/source/file.txt /path/to/destination/
```
Transfers a single file from the source to the destination directory.

### Limiting Bandwidth Usage
```bash
rsync -avz --bwlimit=1000 /source/dir /destination/dir
```
Limits the bandwidth used by rsync to 1000 KBytes per second.



