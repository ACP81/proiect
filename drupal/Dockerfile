FROM ubuntu:bionic
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt upgrade -y
ENV TZ=Europe/Bucharest
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt install software-properties-common wget -y
RUN add-apt-repository ppa:ondrej/php -y && apt update && apt install nginx php-fpm postgresql-client php-pgsql unzip php-xml php-gd php-json php-curl php-mbstring -y
#RUN echo "Instalare Nginx"
#RUN apt install php php-fpm nginx wget drupal -y
RUN wget https://www.drupal.org/download-latest/zip -O /var/www/html/drupal.zip
RUN unzip /var/www/html/drupal.zip -d /var/www/html/
RUN echo "Urmatorul pas va dura foarte mult ! Aveti rabdare !!!"
RUN DRUPAL_FOLDER=`ls -d /var/www/html/*/` && mv ${DRUPAL_FOLDER} /var/www/html/drupal && mkdir /var/www/html/drupal/sites/default/files
RUN cp /var/www/html/drupal/sites/default/default.settings.php /var/www/html/drupal/sites/default/settings.php && cp /var/www/html/drupal/sites/default/default.services.yml /var/www/html/drupal/sites/default/services.yml && chmod a+w /var/www/html/drupal/sites/default/*


RUN rm /var/www/html/drupal.zip
RUN mkdir /run/php
COPY default /etc/nginx/sites-available/
#RUN docker cp </vagrant/drupal/default> <acp81/drupal:latest>:</etc/nginx/sites-available/>
EXPOSE 80
RUN service nginx restart
CMD /usr/sbin/php-fpm8.0 --nodaemonize --fpm-config /etc/php/8.0/fpm/php-fpm.conf & /usr/sbin/nginx -g 'daemon off;'
#COPY drupal /etc/nginx/sites-enabled
#RUN php ./core/scripts/drupal quick-start
#CMD service php-fpm start && nginx
#COPY  in /etc/nginx/sites-available/ 
#ADD ./nginx/dev /etc/nginx/sites-available/
#RUN ln -s /etc/nginx/sites-available/dev /etc/nginx/sites-enabled/dev
#RUN cp ./nginx/dev /etc/nginx/sites-available/
#EXPOSE 80
#CMD ["/bin/bash" "/startup.sh"]


# RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
# RUN rm /etc/nginx/sites-enabled/default
# RUN mkdir -p /var/www/dev/web-front-end/current
# RUN mkdir -p /var/www/dev/api/current
# #ADD ./nginx/dev /etc/nginx/sites-available/
# #RUN ln -s /etc/nginx/sites-available/dev /etc/nginx/sites-enabled/dev
# RUN echo "Instalarea Nginx s-a incheiat"
# CMD service php-fpm start && nginx -g daemon off;
# RUN nginx -t
# #RUN service nginx start
# RUN service nginx status

# RUN echo "Creare director jenkins..."
# RUN mkdir /opt/jenkins
# RUN echo "Descarcare Jenkins..."
# RUN wget https://mirror.gruenehoelle.nl/jenkins/war-stable/latest/jenkins.war -O /opt/jenkins/jenkins.war
# RUN mkdir /opt/jenkins/plugins
# RUN apt-get install unzip -y
# RUN unzip /opt/jenkins/jenkins.war 'WEB-INF/detached-plugins/*' -d tmp/
# RUN cp ./tmp/WEB-INF/detached-plugins/* /opt/jenkins/plugins/
# #RUN echo "/mnt/pg_master/wal_archives     10.20.20.5(rw,sync,no_root_squash)" >> /etc/exports
# RUN echo "Starting Jenkins..."
# ENV JENKINS_HOME=/opt/jenkins
# #ENV JENKINS_OPTS="--httpPort=80"
# ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"
# ENTRYPOINT ["java","-Djenkins.install.runSetupWizard=false","-jar","/opt/jenkins/jenkins.war"]
# CMD ["--httpPort=8080"]
#RUN apt-get install iptables -y
#RUN  iptables -I INPUT 1 -p tcp --dport 8080 -j ACCEPT
#RUN  iptables -I INPUT 1 -p tcp --dport 80 -j ACCEPT
#ENTRYPOINT ["iptables","-A","PREROUTING","-t","nat","-i","eth0","-p","tcp","--dport","80","-j","REDIRECT","--to-port","8080"]


