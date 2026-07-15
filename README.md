1.  For the memory and CPU expansion we can just change the flavor of the current VM On the FusionSphere OM, we can use copy current flavor of the VM and we need change the memory to 262144MB, and 48 vCPU , we just keep other information same as current flavor.
    
2.  Binding the new flavor with the VM in the OM webportal of using command:  
    nova volume-attach VMID disk-ID
    
3.  for the data disk expansion, we need create a new disk first on the FusionSphere OM for example if we want expand the current 1TB to 4TB,we need create a new lun with 3TB first and attach the new LUN to the VM.
    
4.  login to the VM via ssh or console and do the following change in the VM. you will see the new disk via command : lsblk (exmple /dev/vdc)
    A. Initialize the new hard disk(example /dev/vdc). pvcreate /dev/vdc
    
    B. Expand the capacity of the VG(ossvg is example). vgextend ossvg /dev/vdc
    
    C.  Allocate the remaining space to opt_lv( opt_lv is the logical vollume example, you can use command lvdisplay to check .) lvextend -l +100%FREE /dev/ossvg/opt\_lv
    
     D. Expand the file system.                  resize2fs /dev/ossvg/opt_lv
