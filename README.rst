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
    sudo apt install rsync nocache git isync run-one nginx


Install crontab:

.. code-block::

    crontab crontab


Configure automatic mounting of tero:

.. code-block::

    sudo mkdir -p /media/tero
    sudo chmod 544 /media/tero
    echo "/dev/sdb1 /media/tero    ext4    defaults 0   0" | sudo tee -a /etc/fstab


Create and activate the static files site:

.. code-block::

    sudo ln -s /home/sofisa/home_server_static /etc/nginx/sites-available/home_server_static
    sudo ln -s /home/sofisa/home_server_static /etc/nginx/sites-enabled/home_server_static


Reboot with the disk connected.

Ispy installation (more info: https://www.ispyconnect.com/download.aspx)

Locally:

.. code-block::
    scp /home/fisa/devel/home-server/ispy_agent.conf cyrene.local:/home/sofisa/ispy_agent.conf


On Cyrene:

.. code-block::
    sudo mv /home/sofisa/ispy_agent.conf /etc/supervisor/conf.d/

    wget https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
    wget https://ispyfiles.azureedge.net/downloads/Agent_Linux64_2_8_3_0.zip

    sudo dpkg -i packages-microsoft-prod.deb
    sudo add-apt-repository -y ppa:jonathonf/ffmpeg-4

    sudo apt install -y apt-transport-https
    sudo apt install -y dotnet-sdk-3.1 ffmpeg libtbb-dev libc6-dev unzip supervisor

    mkdir /home/sofisa/ispy_agent
    unzip Agent_Linux64_2_8_3_0.zip -d /home/sofisa/ispy_agent

    sudo service supervisor restart


And load the config backup.
