# backup-pool-db
Backup the pool database to a local or remote mounted volumes.

Seven previous copies of the pool database are kept. 

  backup-pool-db -d "DESTINATION DIR" [ -m "MOUNT DEVICE/DIR" ] [-i] [-l file] [-p host]
  -d Where backup gets copied
  -m Mount this device or mountpoint beforehand. Must exist in /etc/fstab
  -i Turn on informational output.  Use multiple times for more verbosity
  -l Log output to file. Turns on -i.
  -p Ping host to check for reachability. Abort if down

See crontab.example for examples of how to run the script.
