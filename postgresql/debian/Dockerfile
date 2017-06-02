FROM debian

# install the necesarry packages
RUN apt-get update && \
  apt-get install -y \
    postgresql-9.4

# run the rest as the postgres user
USER postgres

# create the database and user
RUN /etc/init.d/postgresql start && \
    psql --command "CREATE USER docker WITH SUPERUSER PASSWORD 'docker';" && \
    createdb -O docker playground

# ensure host can connect to postgres correctly
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/9.4/main/pg_hba.conf
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.4/main/postgresql.conf

# expose the 5432 port to outside the container
EXPOSE 5432

# set the default command to run when starting the container
CMD ["/usr/lib/postgresql/9.4/bin/postgres", \
      "-D", "/var/lib/postgresql/9.4/main",  \
      "-c", "config_file=/etc/postgresql/9.4/main/postgresql.conf"]
