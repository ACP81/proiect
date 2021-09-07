FROM ubuntu:bionic
RUN apt update && apt upgrade -y
RUN echo "Instalare Java"
RUN apt install openjdk-11-jdk wget -y
RUN echo "Instalarea Java s-a incheiat"
RUN echo "Creare director jenkins..."
RUN mkdir /opt/jenkins
RUN echo "Descarcare Jenkins..."
RUN wget https://mirror.gruenehoelle.nl/jenkins/war-stable/latest/jenkins.war -O /opt/jenkins/jenkins.war
RUN mkdir /opt/jenkins/plugins
RUN apt-get install unzip -y
RUN unzip /opt/jenkins/jenkins.war 'WEB-INF/detached-plugins/*' -d tmp/
RUN cp ./tmp/WEB-INF/detached-plugins/* /opt/jenkins/plugins/
RUN echo "Starting Jenkins..."
ENV JENKINS_HOME=/opt/jenkins
#ENV JENKINS_OPTS="--httpPort=80"
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"
ENTRYPOINT ["java","-Djenkins.install.runSetupWizard=false","-jar","/opt/jenkins/jenkins.war"]
CMD ["--httpPort=8080"]
#RUN apt-get install iptables -y
#RUN  iptables -I INPUT 1 -p tcp --dport 8080 -j ACCEPT
#RUN  iptables -I INPUT 1 -p tcp --dport 80 -j ACCEPT
#ENTRYPOINT ["iptables","-A","PREROUTING","-t","nat","-i","eth0","-p","tcp","--dport","80","-j","REDIRECT","--to-port","8080"]


