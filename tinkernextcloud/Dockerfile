FROM nextcloud:fpm

# Work-around for jre installs
RUN mkdir -p /usr/share/man/man1

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y default-jre && \
    apt-get install -y libreoffice libreoffice-l10n-de libreoffice-help-de && \
    apt-get install -y ffmpeg imagemagick ghostscript && \
     rm -rf /var/lib/apt/lists/*

# Fix PolicyMap for ImageMagick https://www.allerstorfer.at/nextcloud-install-preview-generator/
RUN sed -i 's/domain="coder" rights="none"/domain="coder" rights="read|write"/g' /etc/ImageMagick-6/policy.xml


