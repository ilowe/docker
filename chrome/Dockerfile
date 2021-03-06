# Run Chrome in a container
# 
# docker run -d \
# 		--net host \
# 		-v /etc/localtime:/etc/localtime:ro \
# 		-v /tmp/.X11-unix:/tmp/.X11-unix \
# 		-e DISPLAY=unix$DISPLAY \
# 		-v $HOME/Downloads:/root/Downloads \
# 		-v $HOME/.config/google-chrome:/data \
# 		-v /dev/shm:/dev/shm \
# 		-v /etc/hosts:/etc/hosts \
# 		--device /dev/snd \
# 		--device /dev/video0 \
# 		--group-add audio \
# 		--group-add video \
# 		--name chrome \
# 		ilowe/chrome --user-data-dir=/data --force-device-scale-factor=1 \
# 		--proxy-server="$proxy" --host-resolver-rules="$map" "$args"

# Base docker image
FROM ubuntu:trusty

ADD https://dl.google.com/linux/direct/google-talkplugin_current_amd64.deb /src/google-talkplugin_current_amd64.deb
ADD https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb /src/google-chrome-stable_current_amd64.deb

# Install Chromium
RUN mkdir -p /usr/share/icons/hicolor && \
	apt-get update && apt-get install -y \
	ca-certificates \
	fonts-liberation \
	gconf-service \
	hicolor-icon-theme \
	libappindicator1 \
	libasound2 \
	libcanberra-gtk-module \
	libcurl3 \
	libexif-dev \
	libgconf-2-4 \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
	libnspr4 \
	libnss3 \
	libpango1.0-0 \
	libv4l-0 \
	libxss1 \
	libxtst6 \
	wget \
	xdg-utils \
	--no-install-recommends && \
	dpkg -i '/src/google-chrome-stable_current_amd64.deb' && \
	dpkg -i '/src/google-talkplugin_current_amd64.deb' \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf /src/*.deb

#COPY local.conf /etc/fonts/local.conf

# Autorun chrome
ENTRYPOINT [ "/usr/bin/google-chrome" ]
CMD [ "--user-data-dir=/data" ]