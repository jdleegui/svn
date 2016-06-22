# svn

-. svnadmin create --fs-type fsfs EMS
   chmod -R g+w /home/svn/EMS
   chown -R nobody.nogroup /home/svn/EMS
   export SVN_EDITOR=/usr/bin/vim
   
$ VISUAL=vim crontab -e
28 17 * * * svnadmin dump /home/svn/EMS | gzip -9 > Downloads/EMS.dump.gz
scp /home/jdleegui/Downloads/EMS.dump.gz jdleegui@mpls:/home/jdleegui/Downloads/EMS_android.dump.160621.gz
