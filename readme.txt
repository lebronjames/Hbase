Hbase1.2.6��װ������ԣ�ʹ��shell����hbase

�ο�Hbase�ٷ��ĵ���http://abloz.com/hbase/book.html


һ�����ض����ư�
http://mirror.bit.edu.cn/apache/hbase/stable/hbase-1.2.6-bin.tar.gz

������ѹ�������Ƶ�/usr/localĿ¼��
tar -zxvf hbase-1.2.6-bin.tar.gz
cp -R hbase-1.2.6 hbase
mv hbase /usr/local

����
�� hbase-env.sh������JAVA_HOME
export JAVA_HOME=/opt/app/jdk

�༭ conf/hbase-site.xml ȥ����hbase.rootdir����ѡ��HBase������д���ĸ�Ŀ¼
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
  <property>
    <name>hbase.rootdir</name>
    <value>file:///opt/migu/hbase/tmp/</value>
  </property>
</configuration>

�ġ�����Hbase
./bin/start-hbase.sh

�塢ҳ����ʣ�http://10.5.2.242:16010/
��������hbase-site.xml�޸Ķ˿ڣ�
jps�鿴Hbase�������
��һ�����̣�HMaster

����Shell����Hbase
./bin/hbase shell

�ߡ� ����һ����Ϊ test �ı������ֻ��һ�� ���� Ϊ cf�������г����еı�����鴴�������Ȼ�����Щֵ��
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
�������Ƿֱ������3�С���һ����keyΪrow1, ��Ϊ cf:a�� ֵ�� value1��HBase�е������� ����ǰ׺���е�������ɵģ���ð�ż����������һ�е���������a.

���������.

�ˡ�Scan�������������
hbase(main):007:0> scan 'test'
ROW        COLUMN+CELL
row1       column=cf:a, timestamp=1288380727188, value=value1
row2       column=cf:b, timestamp=1288380738440, value=value2
row3       column=cf:c, timestamp=1288380747365, value=value3
3 row(s) in 0.0590 seconds

�š�Getһ�У���������
hbase(main):008:0> get 'test', 'row1'
COLUMN      CELL
cf:a        timestamp=1288380727188, value=value1
1 row(s) in 0.0400 seconds

ʮ��disable �� drop ���ű����������ոյĲ���
hbase(main):012:0> disable 'test'
0 row(s) in 1.0930 seconds
hbase(main):013:0> drop 'test'
0 row(s) in 0.0770 seconds 

ʮһ���ر�shell
hbase(main):014:0> exit

ʮ����Hbaseֹͣ�ű�
����ֹͣ�ű���ֹͣHBase.
$ ./bin/stop-hbase.sh










