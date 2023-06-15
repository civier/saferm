# saferm
Folder deletion with safeguards against human error

USAGE

``source path/to/file/setup_saferm.sh SAFEFOLDER``

``saferm FOLDER``

ARGUMENTS

FOLDER - the folder to delete
SAFEFOLDER - the folder to which saferm saves the backup archive (in case FOLDER cannot be deleted in full)

OUTPUT

If FOLDER and all the files and folders below it are deleted in full, the message "saferm: successfuly deleted FOLDER" will be printed.
Otherwise, an error message(s) will be displayed, and if saferm created a backup archive of FOLDER (see scenario 3 below), the archive's name will be given in the output.

NOTES

saferm protects against 3 cases where running 'rm -rf' might have catastrophic outcomes -
1) FOLDER is not writable to user - saferm will do nothing
2) The parent directory of FOLDER is not writable to user - saferm will do nothing
3) The tree below FOLDER contains at least one directory not writable to user - saferm may remove some folders below FOLDER (and the files they contain) that are writable to user. However, the complete content of FOLDER will be available in the tar file created in SAFEFOLER.

saferm does not protect against the case that the user deletes an unitended FOLDER, but all folders in the tree below FOLDER as well as the parent of FOLDER are writable to user.

saferm has multiple advantages comapred with replacing rm with moving files to trash and then removing them:

- the trash folder is usually in the user home directory, and it might be too small to hold the whole of FOLDER. saferm can use any SAFEFOLDER for the backup archive.
- saferm works even if SAFEFOLDER has limited number of unused indoes (only 1 additional inode is necessary for saferm)
- saferm does not leave any traces if FODLER can be removed in full. In that case, the backup archive will be deleted before saferm exits.
- if the trash folder is on another drive than FOLDER, moving files to trash will be implemented as a recdursive copy command, which is slow. saferm only creates a single backup archive file, which is much faster.
- saferm does not require the user to run 'rm -rf' at any point, so it is safer. If rm is replaced with moving files to trash, the user will ultimately need to delete folders in the trash folder using 'rm -rf'
