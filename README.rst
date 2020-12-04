Home Server
-----------

Home server configs and instructions.

Steps to install server
-----------------------

Copy files needed on the server:

.. code-block::

    scp /home/fisa/devel/mios/scripts/update_cyrene_fisadev_com cyrene.local:/home/sofisa/update_cyrene_fisadev_com
    scp /home/fisa/devel/mios/scripts/backup_fisadev_gmail cyrene.local:/home/sofisa/backup_fisadev_gmail
    scp /home/fisa/devel/mios/dotfiles/mbsyncrc_fisadev_gmail cyrene.local:/home/sofisa/mbsyncrc_fisadev_gmail
    scp /home/fisa/devel/mios/sites_nginx/home_server_static cyrene.local:/home/sofisa/home_server_static
    scp /home/fisa/devel/home-server/crontab cyrene.local:/home/sofisa/crontab


Update index and install packages:

.. code-block::

    sudo apt update
    sudo apt install rsync nocache git isync run-one nginx vim tmux


Install crontab:

.. code-block::

    crontab crontab


Configure automatic mounting of tero:

.. code-block::

    sudo mkdir -p /media/tero
    sudo chmod 544 /media/tero
    echo "/dev/sdc1 /media/tero    ext4    defaults 0   0" | sudo tee -a /etc/fstab

(the "sdc1" is the first (1) partition of the third (c) disk device. Check if that's still true in new machines)


Create and activate the static files site:

.. code-block::

    sudo ln -s /home/sofisa/home_server_static /etc/nginx/sites-available/home_server_static
    sudo ln -s /home/sofisa/home_server_static /etc/nginx/sites-enabled/home_server_static


Reboot with the disk connected.

Install motioneye
-----------------

(more info: https://github.com/ccrisan/motioneye/wiki/Installation)

.. code-block::

    sudo apt install motion ffmpeg v4l-utils python-pip python-dev curl libssl-dev libcurl4-openssl-dev libjpeg-dev
    sudo pip install motioneye
    sudo mkdir -p /etc/motioneye
    sudo cp /usr/local/share/motioneye/extra/motioneye.conf.sample /etc/motioneye/motioneye.conf
    sudo mkdir -p /var/lib/motioneye
    sudo cp /usr/local/share/motioneye/extra/motioneye.systemd-unit-local /etc/systemd/system/motioneye.service
    sudo systemctl daemon-reload
    sudo systemctl enable motioneye
    sudo systemctl start motioneye


And load the config backup.
