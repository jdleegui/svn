# svn

-. svnadmin create --fs-type fsfs EMS
   chmod -R g+w /home/svn/EMS
   chown -R nobody.nogroup /home/svn/EMS
   export SVN_EDITOR=/usr/bin/vim
   
$ VISUAL=vim crontab -e
28 17 * * * svnadmin dump /home/svn/EMS | gzip -9 > Downloads/EMS.dump.gz
scp /home/jdleegui/Downloads/EMS.dump.gz jdleegui@mpls:/home/jdleegui/Downloads/EMS_android.dump.160621.gz

svn export http://192.168.123.99/SVN/POINTS/branches/R.2.0_UTRANS7200 utrans7200
svn co http://192.168.123.99/SVN/POINTS/branches/R.2.0_UTRANS7200 utrans7200 --username kkk --password kkk
svn list svn://192.168.123.247/UT7400N/trunk/usermodule/ZebOS_730/lib/ipc
svn st -u

-. sudo apt-get install subversion subversion-tools libapache2-svn
   sudo groupadd svn
   sudo useradd -d /home/svn -g svn svn -m
   sudo vim /etc/apache2/mods-enabled/dav_svn.conf
   sudo htpasswd2 -cm /etc/apache2/dav_svn.passwd svnuser


   svn import test svn://192.168.123.101/sample/trunk --username ems --password ems
   svn list svn://192.168.123.101/sample/ --username ems --password ems
   svn co svn://192.168.123.101/sample/trunk test --username ems --password ems
   
   -. vim /home/svn/EMS/conf/svnserve.conf
   anon-access = none
   auth-access = write
   password-db = passwd
   vim /home/svn/EMS/conf/passwd
   [users]
   jdlee = jdlee
   wjpaek = wjpaek
   bsmoon = bsmoon
   chmod -R a+w /home/svn/EMS


-. client side
   svn mkdir svn://192.168.123.101/EMS/UTrans7200 --username jdlee --password jdlee

. cd UTrans7200
   svn update
   svn add common.h
   svn commit common.h
   svn commit resource.h -F "C:\Temp\msg2.txt"
   svn log -rHEAD
   svn log -r95:85
   svn delete --keep-local Utrans7200.v11.suo
   svn delete --keep-local HTML/UTRANS7200.chm
   svn st --show-update
   svn diff -r HEAD ReadMe.txt
   svn revert
   svn propedit svn:ignore ./Debug
   svnadmin dump EMS > /tmp/EMS_130628_svn.dump
   
   -. svn export -r242 L2Pw.cpp        doc\svn\L2Pw_242.cpp        && windiff L2Pw.cpp        doc\svn\L2Pw_242.cpp
   svn update L2Pw.cpp        && del doc\svn\L2Pw_242.cpp
   svn update > r
   svn update > p >
   svn resolve --accept working test.txt (base, mine-full theirs-full, working)



