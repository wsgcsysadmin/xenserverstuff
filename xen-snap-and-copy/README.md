# xen-snap-and-copy

A script to create backups on local or remote mounted volumes.

The basic process is:
* (optional) Ping remote host before mounting
* Mount (local or remote) volume
* Get VM UUID
* Create snapshot of VM
* Convert snapshot to a template
* Remove or rename previous existing backup
* Copy the snapshot to the volume.
* Delete the snapshot
* (optional) Scan the SR to trigger garbage collection
* Unmount volume

````
  xen-snap-and-copy -v "VM NAME" -d "DESTINATION DIR" [ -m "MOUNT DEVICE/DIR" ] [ -i[i]... ] [-a File name] [-t] [-r] [-n] [-l file] [-p host] [-s]
  -v Name of VM as listed by 'xe vm-list'
  -d Where backup gets copied
  -m Mount this device or mountpoint beforehand. Must exist in /etc/fstab
  -i Turn on informational output.  Use multiple times for more verbosity
  -a Alternmate name for VM to use when creating file
  -t Add a timestamp to the file name
  -r Remove exiting file before copy.(Otherwise will fail). Conflict: -k
  -k Keep previous backup by renaming it with a 'prev_' prefix. Conflict: -r
  -n For Testing. Do not copy the snapshot. Only create and delete it
  -l Log output to file. Turns on -i.
  -p Ping host to check for reachability. Abort if down
  -s Scan SR of VM's VDI after backup
````

See crontab.example for examples of how to run the script.

The root user gets mailed all errors.
