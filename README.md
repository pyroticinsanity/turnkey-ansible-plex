turnkey-ansible-plex
====================

This is an ansible script that can build a Plex server running on a turnkey Linux machine.

How to use it
====================
Grab either the Turnkey Linux VM or the installation ISO and build your machine.
Get ansible on the machine following the steps here: http://docs.ansible.com/intro_installation.html

Make sure you modify ansible_hosts to have the IP address or hostname of the machine. Right now it is set to "plex".
This also has my own custom mount points in it so you'll need to modify plex/tasks/main.yml and either comment out 
the following lines or add your own:
 - name: Add mount points for the media
   mount: name={{ item.name }} src={{ item.src }} fstype=cifs opts=ro,guest,_netdev state=mounted
   with_items:
      - { name: "/mnt/blob", src: "//blob/Volume_2" }


Put these ansible scripts on the ansible machine and run them with the following commands:

cd <root directory of playbook.yml>
ansible-playbook playbook.yml -i ansible_hosts --ask-pass

Enter the root password of your machine and watch it build your server!

Special Thanks
=====================
The guys here for making a Debian repo with the Plex binaries: https://forums.plex.tv/index.php/topic/51427-plex-media-server-for-debian/

