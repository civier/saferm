# safermrf
Folder deletion with safeguards against human error

USAGE

``source path/to/file/setup_safermrf.sh SAFEFOLDER``

``safermrf FOLDER``

ARGUMENTS

FOLDER - the folder to delete

SAFEFOLDER - the folder to which safermrf saves the backup archive

OUTPUT

If FOLDER and all the files and folders below it are deleted in full, the message "safermrf: successfuly deleted FOLDER" will be printed.
Otherwise, an error message(s) will be displayed, and if safermrf created a backup archive of FOLDER (see scenario 3 below), the archive's name will be given in the output.

NOTES

safermrf protects against these 3 cases -
1) FOLDER is not writable to user - safermrf will do nothing
2) The parent directory of FOLDER is not writable to user - safermrf will do nothing
3) The tree below FOLDER contains at least one directory not writable to user - safermrf may remove some folders below FOLDER (and the files they contain) that are writable to user. However, the complete content of FOLDER will be available in the tar file created in SAFEFOLER
  
**In all these cases, running 'rm -rf' may result in the deletion of all folders in the tree below FOLDER which are writable to user**

safermrf does not protect however against the case that the user deletes an unitended FOLDER, but all folders in the tree below FOLDER as well as the parent of FOLDER are writable to user. This might exclude home and project folders from accidental deletion using safermrf, but their subfolders are still at risk.

safermrf has multiple advantages comapred to replacing rm with moving files to trash:

- the trash folder is usually in the user home directory, and it might be too small to hold the whole of FOLDER. safermrf can use any SAFEFOLDER for the backup archive.
- safermrf works even if SAFEFOLDER has limited number of unused indoes (only 1 additional inode is necessary for safermrf)
- safermrf does not leave any traces if FODLER can be removed in full. In that case, the backup archive will be deleted before safermrf exits.
- if the trash folder is on another drive than FOLDER, moving files to trash will be implemented as a recdursive copy command, which is slow. safermrf only creates a single backup archive file, which is much faster.
- safermrf does not require the user to run 'rm -rf' at any point, so it is safer. If rm is replaced with moving files to trash, the user will ultimately need to delete folders in the trash folder using 'rm -rf'

WARNING

safermrf still does not handle missing or improper SAFEFOLDER or FOLDER arguments
