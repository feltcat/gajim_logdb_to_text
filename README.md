**_Note:_** Because I'm running my own servers for serveral years, main development is done at at https://git.ypbind.de/cgit/gajim_logdb_to_text/

----

Convert Gajims chat log database file into text files
==================================================================

## Preface
[Gajim](https://gajim.org/) stores the chat log in an [SQLite](https://sqlite.org) database format in `${HOME}/.gajim/logs.db`
For easier searching and viewing chat logs should be stored in text files.

[gajim\_logdb\_to\_text](https://git.ypbind.de/cgit/gajim_logdb_to_text/) will read chat logs from the SQLite database file and write the logs
into text files inside a directory

---

## Requirements
### Python
[gajim\_logdb\_to\_text](https://git.ypbind.de/cgit/gajim_logdb_to_text/) is written in Python, so Python >=2.6 is required.
The neccessary `sqlite3` Python module is included in the Python "vanilla" installation.

---

## Command line parameters
gajim\_logdb\_to\_text supports the following command line parameters:

  * `-h` or `--help` - shows help text, usage and copyright/license information
  * `-f` or `--no-fd-cache` - disable cacheing of open file descriptors. Default behavior is to keep a list of open output files and close them all when the conversion finnished instead of closeing and reopening the files every time a log message is appended. Usually the default setting will result in _much_ better write performance but the limit of open file descriptors (ulimit -n) must be set accordingly.
  * `-j` or `--no-jid-cache` - disables reading of the ID -> JID mapping from the database once and lookup JID information from memory instead of requesting it from the database. Usually this will result in much faster lookups (and reduce disk I/O on the database file) but may consume large amounts of memory for huge JID lists.

Mandatory arguments are `<name_of_gajim_logs_db>` and `<name_of_output_directory>`, the output directory must already exists.
The name of the output files is `<year>_<moth>_<day>.log` and will be located in:

  * `<output_dir>/rooms/<room_name>/` - for messages in MUC chat
  * `<output_dir>/rooms/<room_name>/<member>/` - for direct messages from MUC member `<member>`
  * `<output_dir>/<bare_jid>/` - for direct (non-MUC) chat messages

---

## License
This program is licenses under [GLPv3](http://www.gnu.org/copyleft/gpl.html).


