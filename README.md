# svn 설치
```
sudo apt-get install subversion subversion-tools libapache2-svn          # svn 서버 설치
sudo groupadd svn                                                        # svn 그룹 생성
sudo useradd -d /home/svn -g svn svn -m                                  # svn 계정 생성
sudo vim /etc/apache2/mods-enabled/dav_svn.conf                          # (옵션) http 사용시 svn 생성
sudo htpasswd2 -cm /etc/apache2/dav_svn.passwd svnuser                   # (옵션) http 사용시 권한 
```
# server side
```
svnadmin create --fs-type fsfs PROJECT                        # PROJECT 디렉토리 생성
chmod -R g+w /home/svn/PROJECT                                # 읽고 쓰도록 허가
chown -R nobody.nogroup /home/svn/PROJECT                     # 아무나 읽고 써라.
export SVN_EDITOR=/usr/bin/vim                                # svn editor를 VI로 지정

vim /home/svn/PROJECT/conf/svnserve.conf                      # 특정 권한 직접 편집
> anon-access = none
> auth-access = write
> password-db = passwd
> vim /home/svn/PROJECT/conf/passwd
> [users]
> jdlee = jdlee
> wjpaek = wjpaek
> bsmoon = bsmoon
> chmod -R a+w /home/svn/PROJECT
```
# svn 저장 및 백업
```
svnadmin dump PROJECT > /tmp/PROJECT_svn.dump                            # 서버 옵션 : PROJECT라는 SVN 디렉토리를 통째로 덤프하기
$ VISUAL=vim crontab -e                                                  # cron 에 주기적으로 등록하기
28 17 * * * svnadmin dump /home/svn/PROJECT | gzip -9 > Downloads/PROJECT.dump.gz
scp /home/steeve/Downloads/PROJECT_svn.dump.gz steeve@mpls:/home/steeve/Downloads/PROJECT_dump.160621.gz
```
# client side
```
svn list svn://sex.com/sample/ --username ems --password ems             # (단순조회용) 파일을 조회함
svn import test svn://sex.com/sample/trunk --username ems --password ems # (단순조회용) 파일을 통째로 가져옴

svn co svn://sex.com/sample/trunk test --username ems --password ems     # (유지관리용) 파일을 받아옴

svn mkdir svn://sex.com/PRJ/NEW --username aa  --password bb             # 클라이언트에서 svn 서버로 디렉토리 생성하기 
svn update                                                               # (*) 아무생각없이 최신 버전으로 갱신
svn update L2Pw.cpp                                                      # 특정 파일만 생신
svn resolve --accept working test.txt                                    # 현재 버전으로 충돌된것 처리하고 업데이트할때
											                             
svn add myfile.c                                                         # 새로운 파일 등록
svn commit myfile.c -F "C:\Temp\msg2.txt"                                # (*) 등록에 대한 로그 등록
svn commit myfile.c -m "awesome"                                         # (*) 등록에 대한 로그 등록
											                             
svn log -rHEAD                                                           # svn 상태 검색
svn log -r95:85                                                          # 특정 버전의 로그만 검색
svn delete --keep-local Utrans7200.v11.suo                               # svn에서 특정 파일 삭제하되 내 PC껀 남겨놓을때
svn st -u                                                                # (*) 통상적인 조회
svn st --show-update                                                     # 갱신된것만 검색
svn diff -r HEAD ReadMe.txt                                              # 내 파일과 최신 버전을 비교
svn revert                                                               # commit 하기전에 add나 delete한것 취소하기
svn propedit svn:ignore ./Debug                                          # debug 폴더는 무시하기
svn export -r242 sex.cpp  doc\sex.cpp                                    # 내 폴더로 임의 버전 받아보기 (유지관리 안됨)
```


