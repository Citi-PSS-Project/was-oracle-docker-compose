FROM buildpack-deps:trusty-curl

MAINTAINER Alexei Ledenev <alexei.led@gmail.com>

ENV PORT_DB_WEB 80180
ENV PORT_DB 1521

COPY chkconfig /sbin/chkconfig
COPY init.ora /
COPY initXETemp.ora /

RUN apt-get update && \
    apt-get install -y libaio1 net-tools bc unixodbc && \
    apt-get autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN ln -s /usr/bin/awk /bin/awk
RUN mkdir /var/lock/subsys
RUN touch /var/lock/subsys/listener
RUN chmod 755 /sbin/chkconfig
RUN ln -sf /proc/mounts /etc/mtab

COPY oracle-shm /etc/init.d/oracle-shm
RUN chmod 755 /etc/init.d/oracle-shm
RUN /etc/init.d/oracle-shm start

COPY ./pkg /tmp
RUN cat /tmp/oracle-xe_11.2.0-1.0_amd64.deba* > /tmp/oracle-xe_11.2.0-1.0_amd64.deb && \
    dpkg --install /tmp/oracle-xe_11.2.0-1.0_amd64.deb && \
    rm /tmp/oracle-xe_11.2.0-1.0_amd64.deb

RUN mv /init.ora /u01/app/oracle/product/11.2.0/xe/config/scripts
RUN mv /initXETemp.ora /u01/app/oracle/product/11.2.0/xe/config/scripts

RUN printf ${PORT_DB_WEB}\\n${PORT_DB}\\noracle\\noracle\\ny\\n | /etc/init.d/oracle-xe configure

RUN echo 'export ORACLE_HOME=/u01/app/oracle/product/11.2.0/xe' >> /etc/bash.bashrc
RUN echo 'export PATH=$ORACLE_HOME/bin:$PATH' >> /etc/bash.bashrc
RUN echo 'export ORACLE_SID=XE' >> /etc/bash.bashrc

# Oracle data volume
VOLUME /usr/lib/oracle/xe/oradata/XE
# Oracle volume for init SQL scripts
VOLUME /etc/entrypoint-initdb.d

EXPOSE ${PORT_DB}
EXPOSE ${PORT_DB_WEB}

COPY start.sh /
RUN chmod 755 /start.sh

CMD /start.sh