FROM hysds/pge-isce_giant

MAINTAINER aria-ops "aria-ops@list.jpl.nasa.gov"
LABEL description="GRFN PGE container"


USER root

RUN pip3 install 'pyproj==1.9.6'
RUN pip install 'pyproj==1.9.6'

USER ops


# copy ariamh code ensure proper permissions, and move dependencies to final locations
COPY . /home/ops/ariamh
RUN set -ex \
 && sudo /usr/bin/pip3 install joblib netcdf4 \
 && sudo rm -rf /root/.cache \
 && sudo chown -R ops:ops /home/ops/ariamh \
 && mv /home/ops/ariamh/spyddder-man /home/ops/verdi/ops/ \
 && mv /home/ops/ariamh/slcp2pm /home/ops/verdi/ops/ \
 && mv /home/ops/ariamh/slcp2cor /home/ops/verdi/ops/ \
 && cd /home/ops/verdi/ops/slcp2pm/src \
 && ./compile.sh \
 && cd /home/ops/verdi/ops/slcp2cor/src \
 && ./compile.sh

# set entrypoint
WORKDIR /home/ops
CMD ["/bin/bash", "--login"]
