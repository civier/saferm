# saferm
Folder deletion with safeguards against human error

USAGE
source path/to/file/setup_saferm.sh
saferm FOLDER

OUTPUT
If FOLDER and all the files and folders below it are deleted in full, the message "saferm: successfuly deleted FOLDER" will be printed.
Otherwise, only some of the files and folders below FOLDER might be deleted. In this case, the complete content of FOLDER will be available in the tar file indicated in the output.

NOTES
saferm protects against 3 cases -
1) FOLDER is not writable to user
2) The parent directory of FOLDER is not writable to user
3) The tree below FOLDER contains directories without write permission to user

saferm does not protect against the case that the user deletes an unitended FOLDER, but all folders in the tree below FOLDER as well as the parent of FOLDER are writable to user.
