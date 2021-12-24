# syntax=docker/dockerfile:1-labs
FROM mcr.microsoft.com/dotnet/sdk:latest

#---------------------------------------------
# BUILD ARGUMENTS
#---------------------------------------------
ARG UID=1000
ARG GID=1000
ARG USERNAME=dev
ARG USERPASSWD=dev
ARG GROUPNAME=dev
ARG SUDOGROUP=%dev
ARG PKGS1="sudo tzdata locales file iputils-ping net-tools psmisc"
ARG PKGS2="make bat vim exuberant-ctags less ncat"

#---------------------------------------------
# ROOT OPERATIONS
#---------------------------------------------
USER root
# >>> Install packages
RUN <<EOF
	apt-get update -q
	DEBIAN_FRONTEND=noninteractive apt-get install -y -q --no-install-recommends ${PKGS1} ${PKGS2}
EOF
# >>> Build locales
RUN <<EOF
	locale-gen ja_JP.UTF-8
	localedef -i ja_JP -c -f UTF-8 -A /usr/share/locale/locale.alias ja_JP.UTF-8
	ln -sf  /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
	rm -rf /var/lib/apt/lists/*
EOF
# >>> Create user with sudo permission
RUN <<EOF
	groupadd -g ${GID} ${USERNAME}
	useradd -m -s /bin/bash -u ${UID} -g ${GID} ${USERNAME}
	echo "${USERNAME}:${USERPASSWD}" | chpasswd
	echo "${SUDOGROUP} ALL=(ALL) ALL" > /etc/sudoers.d/dev
EOF
# >>> Define environments
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja 
ENV LC_ALL ja_JP.UTF-8
ENV TZ Asia/Tokyo

#---------------------------------------------
# NON-ROOT USER OPERATIONS
#---------------------------------------------
USER dev
# >>> Install dotnet packages
RUN <<EOF
EOF
# >>> Misc user operations
RUN <<EOF
	echo 'alias bat=batcat' >> /home/${USERNAME}/.bashrc
	echo 'alias cat=bat' >> /home/${USERNAME}/.bashrc
EOF
# >>> Copy vim config file
COPY ./vimrc.docker /home/${USERNAME}/.vimrc
# >>> Set working directory
WORKDIR /workspace

#---------------------------------------------
# MISC
#---------------------------------------------
EXPOSE 8889
VOLUME /workspace
