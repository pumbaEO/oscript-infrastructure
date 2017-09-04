FROM jenkins:2.60.2

# для автообновления инстанса
# добавить volume для /usr/share/jenkins
#chown jenkins:jenkins /usr/share/jenkins
#chown jenkins:jenkins /usr/share/jenkins/jenkins.war

# slave должен иметь mono
USER root
RUN apt-get clean && apt-get update && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
	&& echo "deb http://download.mono-project.com/repo/debian jessie main" | tee /etc/apt/sources.list.d/mono-official.list \
	&& apt-get update \
	&& apt-get -y install mono-complete

# slave должен иметь docker
RUN curl -sSL https://get.docker.com/ | sh \
	&& usermod -a -G docker jenkins
ENV LANG ru_RU.UTF-8
ENV LANGUAGE ru_RU.UTF-8
ENV LC_MESSAGES "ru_RU.UTF-8"

RUN apt-get update  && apt-get install -y locales \
	language-pack-en \
	language-pack-ru \
	language-pack-ru-base \
	rsync \
	sudo \
	&& apt-get autoclean -y \
	&& rm -rf /var/lib/apt/lists/*
	
#locales
RUN locale-gen ru_RU \
	&& locale-gen ru_RU.UTF-8 \
	&& locale-gen en_US \
	&& update-locale LANG=ru_RU.UTF-8 LANGUAGE=ru_RU

RUN mkdir -p /etc/sudoers.d && \
	echo 'jenkins ALL=(root) NOPASSWD: /usr/bin/rsync' >> /etc/sudoers.d/10-jenkins

USER jenkins
