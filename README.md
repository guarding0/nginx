#!/bin/bash
url="/usr/local/nginx/sbin/nginx"
mkdir /opt/nginx &> /dev/null
mk='/opt/nginx/'
scp  student@192.168.2.254:/linux-soft/02/lnmp_soft/nginx-1.1* $mk
while :
do
read -p "请输入：[1.安装 2.更新 3.退出]  " s
  if [ -z $s ];then
	continue 
  elif [ $s == "1" ];then
    echo "有以下版本可以安装"
    ls /opt/nginx/nginx-* |awk -F\/ '{print NR "--->",$4}'
    fil=`ls /opt/nginx/nginx-* |awk -F\/ '{print NR ":"$4}'`
read -p "请输入要安装的版本：" b1
      for i in $fil
      do
	n=${i%%:*} 
	m=${i##*:}
	e=`echo $m |awk -F\. '{print $1"\."$2"\."$3}' 2> /dev/null`
	[ "$b1" == "$n" ] && tar -xf /opt/nginx/$m && break || continue
      done
	id nginx &> /dev/null || useradd -s /sbin/nologin nginx > /dev/null
	yum -y install gcc pcre-devel openssl-devel &> /dev/null
echo "正在安装，这可能需要1分钟左右..."
	cd $e && ./configure --user=nginx --group=nginx --with-http_ssl_module > /dev/null && make > /dev/null && make install > /dev/null #编译并安装
netstat -ntulp |grep nginx > /dev/null  || $url #启动nginx
systemctl stop firewalld &> /dev/null ; setenforce 0 &> /dev/null
curl http://192.168.2.100
echo "即将安装mariadb、mariadb-server、mariadb-devel | php、php-fpm、php-mysql" ;sleep 3
echo "正在安装mariadb、mariadb-server、mariadb-devel | php、php-fpm、php-mysql..."
yum -y install mariadb mariadb-server mariadb-devel php php-fpm php-mysql > /dev/null
sed -i  '65,71s/#//;/SCRIPT_FILENAME/s/^/#/;s/fastcgi_params/fastcgi.conf/' /usr/local/nginx/conf/nginx.conf
netstat -ntulp |grep nginx > /dev/null && $url -s reload  || $url #重新加载nginx
echo "LNMP部署成功！" && break
  elif [ $s == "2" ];then
		echo "有以下版本可以更新："
    ls /opt/nginx/nginx-* |awk -F\/ '{print NR "--->",$4}'
    fil=`ls /opt/nginx/nginx-* |awk -F\/ '{print NR ":"$4}'`
read -p "请输入要安装的版本：" b1
      for i in $fil
      do
        n=${i%%:*}
        m=${i##*:}
        e=`echo $m |awk -F\. '{print $1"\."$2"\."$3}' 2> /dev/null`
        [ "$b1" == "$n" ] && tar -xf /opt/nginx/$m && break || continue
      done
        id nginx > /dev/null || useradd -s /sbin/nologin nginx > /dev/null
        yum -y install gcc pcre-devel openssl-devel &> /dev/null
while :
do
read -p "请输入要添加的模块或选项：" module
[ ! -z "$module" ] && break || continue
done
echo "花开有时，颓靡无声，最直白的告白莫过于执着的等待..."
cd $e && ./configure $module > /dev/null && make > /dev/null
	cp -f  objs/nginx $url
ss -ntulp |grep nginx > /dev/null && killall -9 nginx && $url || $url #更新软件
  echo "更新成功！" && break
  elif [ $s == "3" ];then
	echo "goodbye!" && sleep 1 && break
  else
	echo "一不小心输错啦！"
  fi
done
