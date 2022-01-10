*Check out: [https://github.com/osquery/osquery](https://github.com/osquery/osquery)*

## Features
- aggregates OS events into relational database
- **osqueryi**: The interactive osquery shell (help / .table / .schema)
- **osqueryd**: A daemon for scheduling and running queries in the background.
- **osqueryctl**: A helper script for testing a deployment or configuration of osquery.

## File Integrity Monitoring (FIM)
1.  `cd /usr/share/osquery/packs`
2.  `touch mypack.conf`
3.  `nano mypack.conf`: define files and paths for FIM
4.  `update /etc/osquery.conf`: adding mypack.conf under "packs"
5.  `set option "enable_file_events": "true"`
6.  `service osqueryd restart`
7.  `osqueryi`:  select target_path,action,atime from file_events;

#### Query Examples

1. `SELECT time, script_text FROM powershell_events;`

2. `SELECT processes.name, process_open_sockets.remote_address, process_open_sockets.remote_port FROM process_open_sockets LEFT JOIN processes ON process_open_sockets.pid = processes.pid WHERE process_open_sockets.remote_port != 0 AND processes.name != '';`

3. `SELECT path, size, from file WHERE path like 'C:Users%%' AND mtime > (select local_time from time) - 100 AND filename != '.'`

4. `SELECT processes.pid, users.username, processes.path from processes LEFT JOIN users ON processes.uid = users.uid WHERE processes.path != '';`
