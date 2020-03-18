FROM ibmcom/ibm-http-server:9.0.5.0
#COPY responsefile.txt /opt/IBM/WebSphere/Toolbox/WCT/ 
#RUN /opt/IBM/WebSphere/Toolbox/WCT/wctcmd.sh -tool pct -defLocPathname /opt/IBM/WebSphere/Plugins -defLocName loc1 -createDefinition -response /opt/IBM/WebSphere/Toolbox/WCT/responsefile.txt
RUN /opt/IBM/HTTPServer/bin/htpasswd -cb /opt/IBM/HTTPServer/conf/admin.passwd ihsadmin ihspasswd
COPY admin.conf /opt/IBM/HTTPServer/conf/admin.conf
