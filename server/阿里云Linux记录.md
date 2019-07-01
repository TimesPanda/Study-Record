```
前言：因为之前一直使用阿里云的云存储服务器，后面忘记使用快照，也因为误操作，导致服务器无法使用。上面配置项那些已经无法回退，只能重新安装。因此记录一下！
```
### 1.在Linux上使用Tomcat
- 先上传Tomcat服务(因为上传的为zip，因此需要解压)
```
 安装ZIP压缩：yum install zip
 解压ZIP文件：yum install unzip
```
- 配置并允许Tomcat
```
可能会遇到权限问题：$ sudo chmod -R 777 某一目录
```
- 打开端口
```
需要打开阿里云端口
```

### 2.自动备份机制
```
因为之前服务器奔溃过一次，因此想着来备份一下服务器上的数据库内容
```
- 第一步，编写crontab脚本（这里省去脚本开启、安装的过程等）
```
#!/bin/bash

USER="XXXX"
PASSWORD="XXXX"
DATABASE="platform"
HOSTNAME="172.17.178.18"

OPTIONS="-h$HOSTNAME -u$USER -p$PASSWORD $DATABASE"

# 备份路径
BACKUP_PATH=/home/mysql_backup/

# 备份记录路径
BACKUP_INFO=/home/mysql_backup/backup_info.log

# 备份文件名
FILE_NAME=$DATABASE"_"`date '+%Y%m%d_%H%M%S'`.sql

# 备份路径不存在则创建
if [ ! -d $BACKUP_PATH ] ; then
	mkdir -p "$BACKUP_PATH"
fi

# 开始备份
echo " " >> $BACKUP_INFO
echo "-----------------------------------------" >> $BACKUP_INFO
echo "BACKUP DATE:" $(date +"%y-%m-%d %H:%M:%S") >> $BACKUP_INFO
echo "-----------------------------------------" >> $BACKUP_INFO
cd $BACKUP_PATH
mysqldump $OPTIONS > $FILE_NAME
if [[ $? == 0 ]]; then
    tar czvf $FILE_NAME.tgz $FILE_NAME >> $BACKUP_INFO 2>&1
    echo "$FILE_NAME.tgz Backup Successful!" >> $BACKUP_INFO
    rm -f $FILE_NAME
else
    echo "Database Backup Failed!" >> $BACKUP_INFO
fi
echo "BACKUP END :" $(date +"%y-%m-%d %H:%M:%S") >> $BACKUP_INFO
echo " " >> $BACKUP_INFO
echo "Backup Process Done!"
```
- 第二步骤，开启自动任务，我这里采用每天凌晨备份
```
测试每十分钟执行一次，成功！
# crontab -e
0,10,20,30,40,50 * * * * /temp/timer.sh

每天凌晨执行：
1 0 * * * /home/linrui/XXXX.sh
```
- 查看相关的任务信息，可以查看crontab命令，比如：-e 表示编辑，-l 表示查看任务列表等
