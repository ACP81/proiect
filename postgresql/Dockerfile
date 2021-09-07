# syntax=docker/dockerfile:1
FROM ubuntu:bionic
RUN apt-get update  && apt-get install wget gnupg2 sudo -y
ENV TZ=Europe/Bucharest
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc |apt-key add -
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main" |tee /etc/apt/sources.list.d/pgdg.list

RUN apt-get update && apt-get install -y  software-properties-common postgresql-12 postgresql-client-12 postgresql-contrib-12

USER postgres

# Create a PostgreSQL role named ``drupal`` with ``drupal`` as the password and
# then create a database `drupal` owned by the ``drupal`` role.

RUN    /etc/init.d/postgresql start &&\
    psql --command "CREATE USER drupal WITH SUPERUSER PASSWORD 'drupal';" &&\
    createdb -O drupal drupal

RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/12/main/pg_hba.conf

RUN echo "listen_addresses='*'" >> /etc/postgresql/12/main/postgresql.conf

EXPOSE 5432

VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

CMD ["/usr/lib/postgresql/12/bin/postgres", "-D", "/var/lib/postgresql/12/main", "-c", "config_file=/etc/postgresql/12/main/postgresql.conf"]