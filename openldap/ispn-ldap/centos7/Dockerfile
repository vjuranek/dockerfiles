FROM centos:7
MAINTAINER vjuranek <vjuranek@redhat.com>

RUN yum -y update && \
    yum -y install openldap openldap-clients openldap-servers && \
    yum clean all

RUN sed -i s/dc=my-domain,dc=com/dc=infinispan,dc=org/ /etc/openldap/slapd.d/cn=config/olcDatabase\=\{2\}hdb.ldif
RUN sed -i '/olcRootDN: cn=Manager,dc=infinispan,dc=org/a olcRootPW: {SSHA}+c+1pwQwQbhkvgWAWWOIt5la9Vk6PX+S' /etc/openldap/slapd.d/cn=config/olcDatabase\=\{2\}hdb.ldif
RUN sed -i s/dc=my-domain,dc=com/dc=infinispan,dc=org/ /etc/openldap/slapd.d/cn=config/olcDatabase\=\{1\}monitor.ldif
RUN sed -i '$a olcAccess: {0}to attrs=userPassword by self write by dn.base="cn=Manager,dc=infinispan,dc=org" write by anonymous auth by * none' /etc/openldap/slapd.d/cn=config/olcDatabase\=\{2\}hdb.ldif
RUN sed -i '$a olcAccess: {1}to * by dn.base="cn=Manager,dc=infinispan,dc=org" write by self write by * read' /etc/openldap/slapd.d/cn=config/olcDatabase\=\{2\}hdb.ldif


# ADD ldif/conf.ldif /tmp/conf.ldif
# ADD ldif/monitor.ldif /tmp/monitor.ldif
# ADD ldif/ispn.ldif /tmp/ispn.ldif

# RUN ldapmodify -x -H ldapi:/// -f /tmp/conf.ldif && \
#     ldapmodify -x -H ldapi:/// -f /tmp/monitor.ldif 

EXPOSE 389
CMD ["/usr/sbin/slapd","-u","ldap","-d","1"]
