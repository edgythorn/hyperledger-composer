FROM ubuntu:16.04

ENV username=composer 
ENV PATH="/home/${username}/.nvm/versions/node/v8.11.3/bin:${PATH}"

COPY prereqs-ubuntu.sh /home/$username/prereqs-ubuntu.sh

RUN apt-get update && \
    apt-get install -y apt-utils && \
    apt-get install -y curl && \
    apt-get install -y sudo && \
    apt-get install -y software-properties-common && \
    #
    passwd -d root && \
    useradd $username && \
    passwd -d $username && \
    usermod -aG sudo $username && \
    #mkdir /home/$username && \
    chown $username /home/$username && \
    chown $username /home/$username/prereqs-ubuntu.sh && \
    chmod u+x /home/$username/prereqs-ubuntu.sh

USER $username
# prerequisites
RUN /home/$username/prereqs-ubuntu.sh
# need to relogin
RUN exit
# packages
RUN npm install -g composer-cli && \
    npm install -g composer-rest-server && \
    npm install -g generator-hyperledger-composer && \
    npm install -g yo && \
    npm install -g composer-playground 
#clear
RUN rm -f /home/$username/prereqs-ubuntu.sh

RUN exit

WORKDIR /home/$username

CMD ["bash"]
