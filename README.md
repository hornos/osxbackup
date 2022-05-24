## Description
Simple personal `HOME` directory backup script for OS X. Files `rsync -a` copied 
to an encrypted ZFS volume. Arbitrary file or directory patterns can be excluded by
`rofs-filtered` (https://github.com/gburca/rofs-filtered) overlay fs.

## Installation
```bash
mkdir $HOME/local
cd $HOME/local
git clone https://github.com/hornos/osxbackup.git
cd $HOME/local/osxbackup
cd brew
git clone https://github.com/osxfuse/fuse.git
cp fuse/include/*.h /opt/homebrew/include/
brew install rsync
brew install macfuse
brew install ./rofs-filtered.rb
```

You also need to install OpenZFS on OS X (https://openzfsonosx.org/)

## Preparing backup disk
1. Create an encrypted ZFS volume with name `backup`
2. Create a directory with your username under `backup`
3. Create an empty file `backup/$USER/.mounted`

## Creating a backup
Edit '/etc/filter.rc' to specify what to exclude / include in the backup.

```bash
# List available pools
bin/backup a
# Do a backup (select a pool from the list)
bin/backup f <pool>
```
