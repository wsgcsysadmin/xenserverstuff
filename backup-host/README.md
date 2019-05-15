# backup-host
Backup a host server to a local or remote mounted volume.

````
  backup-host -h host-name -d "DESTINATION DIR" [ -m "MOUNT DEVICE/DIR" ]  [-l file] [-p host]
  -h host to backup
  -d Where backup gets copied
  -m Mount this device or mountpoint beforehand. Must exist in /etc/fstab
  -l Log output to file.
  -p Ping host to check for reachability. Abort if down
````

See crontab.example for examples of how to run the script.
