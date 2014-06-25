FROM chocobozzz/diaspora-docker:without_http_sql
MAINTAINER Florian Bigard <florian.bigard@gmail.com>

ENV POSTGRESQLTMPROOT temprootpass

# Install Apache
RUN apt-get -y install apache2

# Install PostgreSQL
RUN apt-get install -y libpq-dev postgresql-9.1 sudo

RUN apt-get clean

ADD install.sh /home/diaspora/install.sh
ADD install_diaspora.sh /home/diaspora/install_diaspora.sh
ADD start.sh /home/diaspora/start.sh

ONBUILD ADD database.yml  /home/diaspora/diaspora/config/database.yml
ONBUILD ADD diaspora.yml  /home/diaspora/diaspora/config/diaspora.yml
ONBUILD ADD diaspora.crt  /home/diaspora/diaspora.crt
ONBUILD ADD diaspora.key  /home/diaspora/diaspora.key
ONBUILD RUN /home/diaspora/install.sh

ONBUILD ADD diaspora.conf /etc/apache2/sites-enabled/000-default.conf
ONBUILD RUN a2enmod ssl proxy proxy_balancer proxy_http headers rewrite

ONBUILD EXPOSE 80
ONBUILD EXPOSE 443
ONBUILD CMD ["/bin/bash", "/home/diaspora/start.sh"] 