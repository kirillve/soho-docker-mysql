FROM mariadb:10.5

RUN apt-get update && \
    apt-get install -y \
        gcc \
        git \
        libmysqlclient-dev

RUN cd /tmp \
    && git clone https://github.com/mysqludf/lib_mysqludf_sys.git \
    && cd lib_mysqludf_sys \
    && gcc -fPIC -Wall -m64 -I/usr/include/mysql -I. -shared lib_mysqludf_sys.c -o /usr/lib/mysql/plugin/lib_mysqludf_sys.so \
    && cp -f ./lib_mysqludf_sys.sql /docker-entrypoint-initdb.d/ \
    && cd /tmp \
    && rm -fr lib_mysqludf_sys

RUN apt remove -y \
    git \
    gcc \
    && rm -rf /var/lib/apt/lists/*
