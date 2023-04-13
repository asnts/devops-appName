FROM =atlassian/bamboo-agent-base:7.2


# Make full package install & cleanup in one docker RUN statement
# to avoid large leftovers in docker image history & cache
# install curl & jq

#RUN apt-get update && \
#   apt-get dist-upgrade -yqq && \
#  apt-get install -y curl wget openssh-client software-properties-common apt-utils sudo && \
#    apt-get autoremove --purge -y && \
#    apt-get clean && \
#    rm /var/lib/apt/lists/*.* && \
#    rm -fr /tmp/* /var/tmp/*

RUN apt-get update -y &&\
  apt-get install -y --no-install-recommends curl jq bash dnsutils ca-certificates && \
 apt-get autoremove -y && \
 apt-get clean -y && \
 rm -rf /tmp/* /var/tmp/* /var/cache/apt/archives/* /var/lib/apt/lists/*

CMD ["tail", "-F", "-n0", "/etc/hosts" ]       


#install node 
    RUN ( curl -sL https://deb.nodesource.com/setup_8.x | bash - ) && \
    apt-get install -y nodejs && \
    apt-get clean && \
    rm /var/lib/apt/lists/*.* && \
    rm -fr /tmp/* /var/tmp/*

#install maven
ENV V_MAVEN3 3.5.3
RUN cd /srv && \
    curl -sL http://mirror.synyx.de/apache/maven/maven-3/$V_MAVEN3/binaries/apache-maven-$V_MAVEN3-bin.tar.gz | tar -xz && \
    ln -s apache-maven-$V_MAVEN3 maven-3.x


#install nodejs
ENV V_NODE_4 4.9.1
RUN cd /srv && \
    wget -nv https://nodejs.org/download/release/latest-v4.x/node-v$V_NODE_4-linux-x64.tar.xz && \
    tar xf node-v$V_NODE_4-linux-x64.tar.xz && \
    rm node-v$V_NODE_4-linux-x64.tar.xz && \
    ln -s node-v$V_NODE_4-linux-x64 node-4.x

#install java jdk

# Mark Oracle license accepted
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections
RUN echo oracle-java10-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
                    build-essential \
                    git subversion \
                    oracle-java8-installer \
                    oracle-java8-set-default \
                    oracle-java8-unlimited-jce-policy \
                    oracle-java10-installer \
                    groovy \
                    graphviz && \
    apt-get autoremove --purge -y && \
    apt-get clean && \
    rm -fr /var/cache/oracle-jdk* && \
    rm /var/lib/apt/lists/*.* && \
    rm -fr /tmp/* /var/tmp/*

