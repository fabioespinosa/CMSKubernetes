FROM cmssw/cmsweb
MAINTAINER Valentin Kuznetsov vkuznet@gmail.com

RUN yum install -y cern-hadoop-config spark-bin-2.3.0 hadoop-bin-2.7.5 hbase-bin-1.2.6 sqoop-bin-1.4
RUN yum install -y java-1.8.0-openjdk-devel

ENV WDIR=/data
ADD scripts $WDIR/sqoop
ADD queries $WDIR/sqoop/queries
ADD run.sh $WDIR/sqoop
ADD daemon.sh $WDIR/sqoop
ADD cronjobs.txt $WDIR/sqoop
RUN hadoop-set-default-conf.sh analytix
RUN source hadoop-setconf.sh analytix
ENV PATH $PATH:/usr/hdp/hadoop/bin:/usr/hdp/sqoop/bin
RUN mkdir -p $WDIR/sqoop/log
WORKDIR $WDIR/sqoop
RUN ln -s /etc/cmsdb/cmsr_cstring
RUN ln -s /etc/cmsdb/lcgr_cstring
RUN crontab cronjobs.txt
