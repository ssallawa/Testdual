FROM oraclelinux:7.6

COPY public-yum-ol7.repo.sav /etc/yum.repos.d/public-yum-ol7.repo
RUN yum -y install cronie mailx vim postgresql-devel python3-pip zip unzip oracle-instantclient18.3-basic oracle-instantclient18.3-devel oracle-instantclient18.3-jdbc oracle-instantclient18.3-sqlplus
# Not required...RUN mkdir /opt/spark

#SBT is similar to Maven..Do we really need this??

#RUN mkdir /opt/sbt
#COPY binaries/sbt-1.3.9.zip /opt/sbt -- Where are we copying the sbt-1.3.9.zip to binaries
#RUN cd /opt/sbt && unzip sbt-1.3.9.zip && rm sbt-1.3.9.zip



ADD binaries/jre-8u241-linux-x64.rpm /root
RUN rpm -ivh /root/jre-8u241-linux-x64.rpm


#COPY binaries/spark-2.4.4-bin-hadoop2.7.tgz /opt/spark
#RUN cd /opt/spark && tar xvzf  spark-2.4.4-bin-hadoop2.7.tgz && rm spark-2.4.4-bin-hadoop2.7.tgz


RUN pip3 install --upgrade pip
RUN pip3 install numpy pandas oci cx_Oracle psycopg2-binary
#pyspark removed


#COPY spark-env.sh /opt/spark/spark-2.4.4-bin-hadoop2.7/conf

#COPY sparkjob /opt/sparkjob
#RUN mkdir -p /root/.oci && mkdir -p /opt/sparkjob/etl_logs
#RUN mkdir -p /opt/sparkjob/scala_etl/lib
#COPY binaries/*.jar /opt/sparkjob/scala_etl/lib/

COPY binaries/*.jar /opt/adwjob/lib
# Where we are creating orahome directory
COPY wallets /opt/orahome 

#ENV SPARK_HOME /opt/spark/spark-2.4.4-bin-hadoop2.7

#ENV PATH $PATH:/opt/sbt/sbt/bin:/usr/lib/oracle/18.3/client64/bin:$SPARK_HOME/bin:$SPARK_HOME/sbin
ENV PATH $PATH:/opt/sbt/sbt/bin:/usr/lib/oracle/18.3/client64/bin
ENV LD_LIBRARY_PATH /usr/lib/oracle/18.3/client64/lib
ENV PYTHONPATH="${PYTHONPATH}:/opt/adwjob"
ENV TNS_ADMIN=/opt/orahome

#RUN cd /opt/sparkjob/scala_etl && ./build.sh


ADD ./start_cron.sh /start_cron.sh
RUN chmod +x /start_cron.sh
CMD ["/bin/bash", "/start_cron.sh"]

