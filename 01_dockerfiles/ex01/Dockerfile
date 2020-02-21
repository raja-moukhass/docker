FROM debian

EXPOSE 9987/udp 10011 30033

# Install Required Packages
RUN apt-get update
RUN apt-get upgrade
RUN apt-get install tar -y
RUN apt-get install wget -y
RUN apt-get install bzip2 -y

# Install Teamspeak
RUN wget http://dl.4players.de/ts/releases/3.8.0/teamspeak3-server_linux_amd64-3.8.0.tar.bz2
RUN tar xvf teamspeak3-server_linux_amd64-3.8.0.tar.bz2
RUN rm -rf teamspeak3-server_linux_amd64-3.8.0.tar.bz2

# RUN SERVER 
WORKDIR  teamspeak3-server_linux_amd64
RUN touch .ts3server_license_accepted

CMD ["./ts3server"]
# docker build -t ex01 .
# docker run -p 9987:9987/udp -p 10011:10011 -p 30033:30033 -it ex01
