Hbase1.2.6安装部署测试，使用shell操作hbase

参考Hbase官方文档：http://abloz.com/hbase/book.html


一、下载二进制包
http://mirror.bit.edu.cn/apache/hbase/stable/hbase-1.2.6-bin.tar.gz

二、解压包，并移到/usr/local目录下
tar -zxvf hbase-1.2.6-bin.tar.gz
cp -R hbase-1.2.6 hbase
mv hbase /usr/local

三、
在 hbase-env.sh中配置JAVA_HOME
export JAVA_HOME=/opt/app/jdk

编辑 conf/hbase-site.xml 去配置hbase.rootdir，来选择HBase将数据写到哪个目录
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
  <property>
    <name>hbase.rootdir</name>
    <value>file:///opt/migu/hbase/tmp/</value>
  </property>
</configuration>

四、启动Hbase
./bin/start-hbase.sh

五、页面访问：http://10.5.2.242:16010/
（可以在hbase-site.xml修改端口）
jps查看Hbase启动情况
多一个进程：HMaster

六、Shell操作Hbase
./bin/hbase shell

七、 创建一个名为 test 的表，这个表只有一个 列族 为 cf。可以列出所有的表来检查创建情况，然后插入些值。
hbase(main):003:0> create 'test', 'cf'
0 row(s) in 1.2200 seconds
hbase(main):003:0> list 'table'
test
1 row(s) in 0.0550 seconds
hbase(main):004:0> put 'test', 'row1', 'cf:a', 'value1'
0 row(s) in 0.0560 seconds
hbase(main):005:0> put 'test', 'row2', 'cf:b', 'value2'
0 row(s) in 0.0370 seconds
hbase(main):006:0> put 'test', 'row3', 'cf:c', 'value3'
0 row(s) in 0.0450 seconds
以上我们分别插入了3行。第一个行key为row1, 列为 cf:a， 值是 value1。HBase中的列是由 列族前缀和列的名字组成的，以冒号间隔。例如这一行的列名就是a.

检查插入情况.

八、Scan这个表，操作如下
hbase(main):007:0> scan 'test'
ROW        COLUMN+CELL
row1       column=cf:a, timestamp=1288380727188, value=value1
row2       column=cf:b, timestamp=1288380738440, value=value2
row3       column=cf:c, timestamp=1288380747365, value=value3
3 row(s) in 0.0590 seconds

九、Get一行，操作如下
hbase(main):008:0> get 'test', 'row1'
COLUMN      CELL
cf:a        timestamp=1288380727188, value=value1
1 row(s) in 0.0400 seconds

十、disable 再 drop 这张表，可以清除你刚刚的操作
hbase(main):012:0> disable 'test'
0 row(s) in 1.0930 seconds
hbase(main):013:0> drop 'test'
0 row(s) in 0.0770 seconds 

十一、关闭shell
hbase(main):014:0> exit

十二、Hbase停止脚本
运行停止脚本来停止HBase.
$ ./bin/stop-hbase.sh










