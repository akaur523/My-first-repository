#!/usr/bin/env python3
#backupVM.py
# Purpose: Back up virtual machines
#
# USAGE: ./backupVM.py
#
# Author: *** Aishween Kaur ***

import os

currentuser = os.popen('whoami')

if currentuser.read().strip() != 'root':
  print('You must be root, current user is: ' + str(currentuser))
  exit()

answer = input("Backup all VMs? (y|n):") # prompt if all VMs to be backed-up

if answer == "y":  # Backup all VMs if answer is yes
 for num in {1,2,3} : # Determinant loop for 3 arguments: 1, 2, and 3
   print("Backing up VM " + str(num))
   os.system('gzip < /var/lib/libvirt/images/centos' + str(num) + '.qcow2 > /home/akaur523/backups/centos' + str(num) + '.qcow2.gz')
   print("VM" + num + "BACKUP DONE")

elif answer == "n" :
 numanswer =  input('Which VM should be backed up? (1/2/3): ')
 while numanswer not in ["1", "2", "3"]:
  numanswer = input("Invalid Selection. Select 1, 2, or 3: ")
  
 print ("Backing up VM" + str(numanswer))
 os.system("gzip < /var/lib/libvirt/images/centos" + str(numanswer) +  ".qcow2 > /home/akaur523/backups/centos" + str(numanswer) + ".qcow2.gz")
 print("VM" + str(numanswer) + "BACKUP DONE")

