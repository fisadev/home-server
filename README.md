# Home Server

Home server configs and instructions.

# Steps to install server:

Copy files needed on the server:

.. code-block::

    scp /home/fisa/devel/mios/scripts/update_cyrene_fisadev_com cyrene:/home/sofisa/update_cyrene_fisadev_com
    scp /home/fisa/devel/mios/scripts/backup_fisadev_gmail cyrene:/home/sofisa/backup_fisadev_gmail
    scp /home/fisa/devel/mios/dotfiles/mbsyncrc_fisadev_gmail cyrene:/home/sofisa/mbsyncrc_fisadev_gmail
    scp /home/fisa/devel/home-server/crontab cyrene:/home/sofisa/crontab


Update index and install packages:

.. code-block::

    sudo apt update
    sudo apt install rsync nocache git isync run-one


Install crontab:

.. code-block::

    crontab crontab


Configure automatic mounting of tero:

.. code-block::

    sudo mkdir -p /media/tero
    sudo chmod 544 /media/tero
    echo "/dev/sdb1 /media/tero    ext4    defaults 0   0" | sudo tee -a /etc/fstab

Reboot with the disk connected.
