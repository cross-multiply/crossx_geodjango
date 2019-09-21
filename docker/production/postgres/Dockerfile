FROM postgres:11.3

# ADD ./dumps/dump.psql\ /docker-entrypoint-initdb.d

COPY ./db/dumps/ /usr/local/bin/dumps/
# COPY ./docker/production/postgres/maintenance /usr/local/bin/maintenance
# RUN chmod +x /usr/local/bin/maintenance/*
# RUN mv /usr/local/bin/maintenance/* /usr/local/bin \
#     && rmdir /usr/local/bin/maintenance

