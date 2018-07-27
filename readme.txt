#Hadoop之spark-sql安装及使用

注：此版本可以与原生HADOOP、CDH5.12.1版本完美兼容；

spark-sql安装步骤：

   1、下载Apache官网spark版本为2.1.0的安装包spark-2.1.0-bin-hadoop2.6.tgz（官方给出的都是已经编译完成的可以拿来直接使用）；
   CDH自带的Spark都是没有带Hive的，若直接运行./spark-sql，会报错，解决方法，将CDH中的hive-site.yml配置文件cp到spark中的conf目录中；
   2、测试
   运行spar-sql后，可以通过浏览器：http://localhost:4040界面查看相应的输出结果等信息；
   3、配置数据源：
   将spark安装目录下conf中的hive-site.xml修改如下信息：
   <property>
    <name>hive.metastore.uris</name>
    <value>thrift://当前系统的IP或者是别名:9083</value>
  </property>
    
    修改完成后，重新运行spark-sql即可；
    
    4、如果运行sql时，出现如下错误时，不要惊慌，
      ***********ERROR SparkSQLDriver:**********************
      请参考修改如下配置：
      <property>
      <name>hive.fetch.task.conversion</name>
      <value>none</value>
      </property>
      修改完成后，重新运行spark-sql，所有功能正常；
      5、为了不影响其他正在使用的spark相关命令，通过软连接的形式将spark-sql命令连接到/usr/bin下，
      ln -s /data/software/spark-2.1.0-bin-hadoop2.6/bin/spark-sql /usr/bin/spark-sql
      注：直接连接后，是无法执行的，原因是由于该命令的家目录不在/usr/bin下，可以通过修改spark-sql中的家目录来解决，具体配置如下：
      SPARK_HOME=/data/software/spark-2.1.0-bin-hadoop2.6
      
      修改完成后，重新执行；
