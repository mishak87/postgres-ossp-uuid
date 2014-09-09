FROM postgres:9.3

RUN apt-get update && apt-get install -y libossp-uuid-dev

RUN ./configure --with-ossp-uuid
RUN make -j"$(nproc)"
RUN chown -R postgres src/test/regress \
&& gosu postgres make check \
|| { cat >&2 /usr/src/postgres/src/test/regress/log/initdb.log; false; }
RUN make install
RUN make clean
