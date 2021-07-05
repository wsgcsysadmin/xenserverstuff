= RESTORE A VM

Example:
  [root@xen-2 ~]#  xe vm-import filename=/backup-es/BACKUP-ETL.ova force=true sr-uuid=b2e170c4-5eec-adc1-586a-6486a3372544 

The SR UUID needs to be set to the target SR. I suggest using a local SR and
then moving the VM to the iSCSI SR.

= RESTORE A DISK

Disk image file names have this format:
   BACKUP-{vmname}_{diskname}.{size}.vdi

First, get the size of the VHD file:
  [root@xen-2 ~]# ls -l /backup-es/BACKUP-svr_disk0.vhd
  -rw------- 1 root root 1734787072 Jul  4 06:57 /backup-es/BACKUP-citlicsvr_citlicsvr-disk0.8589934592.vdi

The size is the number between the periods in the file name: 8589934592
Do NOT use the actual VHD file size because it does not represent the size
of the filesystem in the image.

Create a VDI on an SR using size_vdi for the virtual-size parameter:
  [root@xen-2 ~]# xe vdi-create name-label=zzztest sr-uuid=a26107b8-f853-028f-8a2a-52e7d40d3b02 type=user virtual-size=8589934592
  1d64f4aa-b400-471a-97af-1003b370b599

It returns the UUID of the new VDI: 1d64f4aa-b400-471a-97af-1003b370b599

Check the UUID to make sure it is the VDI you wish to overwrite:
  [root@xen-2 ~]# xe vdi-list uuid=1d64f4aa-b400-471a-97af-1003b370b599
  uuid ( RO)                : 1d64f4aa-b400-471a-97af-1003b370b599
            name-label ( RW): citlicsvr-disk0
      name-description ( RW): 
               sr-uuid ( RO): a26107b8-f853-028f-8a2a-52e7d40d3b02
          virtual-size ( RO): 8589934592
              sharable ( RO): false
             read-only ( RO): false

Do the import:
  [root@xen-2 ~]# xe vdi-import filename=/backup-es/BACKUP-citlicsvr_citlicsvr-disk0.vdi format=vhd progress=true uuid=1d64f4aa-b400-471a-97af-1003b370b599
  [|] ######################################################> (100% ETA
  00:00:00) 
  Total time: 00:00:23

  