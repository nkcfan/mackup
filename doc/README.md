# Configuration

## Storage

### Dropbox

You can specify the storage type Mackup will use to store your configuration
files.
For now you have 3 options: `dropbox`, `google_drive` and `file_system`.
If none is specified, Mackup will try to use the default: `dropbox`.
With the `dropbox` storage engine, Mackup will automatically figure out your
Dropbox folder.

```ini
[storage]
engine = dropbox
```

### Google Drive

If you choose the `google_drive` storage engine instead, Mackup will figure out
where your Google Drive is and store your configuration files in it.

```ini
[storage]
engine = google_drive
```

### File System

If you want to specify another directory, you can use the `file_system` engine
and Mackup won't try to detect any path for you: it will store your files where
you explicitely told him to, using the `path` setting.
The `path` can be absolute (from the `/` of your drive) or relative to your
home directory.
The `path` setting is mandatory when using the `file_system` engine.

```ini
[storage]
engine = file_system
path = some/folder/in/your/home
# or path = /some/folder/in/your/root
```

### Custom Directory Name

You can customize the directory name in which Mackup stores your file. By
default, if not specified, Mackup creates a `Mackup` directory in the storage
engine you chose, e.g. `~/Dropbox/Mackup`.

```ini
[storage]
directory = Mackup
```

For example:

```ini
[storage]
engine = file_system
path = dotfiles
directory = backup
```

This will store your files in the `~/dotfiles/backup` directory in your home.

## Applications

### Only sync one or two application

In your home folder, create a file named `.mackup.cfg` and add the application
names to allow in the `[applications_to_sync]` section, one by line.

```ini
# Example, to only sync SSH and Adium:
[applications_to_sync]
ssh
adium
```

A [sample](.mackup.cfg) of this file is available in this folder. Just copy it
in your home folder:

```bash
$ cp mackup/doc/.mackup.cfg ~/
```

### Don't sync an application

In your home folder, create a file named `.mackup.cfg` and add the application
names to ignore in the `[applications_to_ignore]` section, one by line.

```ini
# Example, to not sync SSH and Adium:
[applications_to_ignore]
ssh
adium
```

A [sample](.mackup.cfg) of this file is available in this folder. Just copy it
in your home folder:

```bash
$ cp mackup/doc/.mackup.cfg ~/
```

### Get official support for an application

Open a [new issue](https://github.com/lra/mackup/issues) and ask for it, or
fork Mackup and open a
[Pull Request](https://help.github.com/articles/using-pull-requests).
The stock application configs are in the `mackup/applications` directory.

### Add support for an application or any file or directory

You can customize the Mackup engine and add support for unsupported
applications or just custom files and directories you'd like to sync.

Let's say that you'd like to add support for Nethack (config file:
`.nethackrc`) and for the `bin` and `.hidden` directories you keep in your
home.

In your home, create a `.mackup` directory and add a config file for the
application you'd like to support.

```bash
$ mkdir ~/.mackup
$ touch ~/.mackup/nethack.cfg
$ touch ~/.mackup/my-files.cfg
```

Edit those files

```bash
$ cat ~/.mackup/nethack.cfg
[application]
name = Nethack

[configuration_files]
.nethackrc
```

```bash
$ cat ~/.mackup/my-files.cfg
[application]
name = My personal synced files and dirs

[configuration_files]
bin
.hidden
```

You can run mackup to see if they are listed
```bash
$ mackup list
Supported applications:
[...]
 - my-files
 - nethack
[...]
```

All good, you can now sync your newly configured files:
```bash
mackup backup
```

If you override an application config that is already supported by Mackup, your
new config for this application will replace the one provided by Mackup.

You can find some sample config in this directory.
