FROM datasnap-io/iotivity-full

COPY Thermostat.cpp /root/Thermostat.cpp
COPY thermostat_db.json /root/thermostat_db.json
COPY Makefile /root/Makefile
COPY runThermostat.sh /root/runThermostat.sh

RUN chmod +x /root/runThermostat.sh

WORKDIR /root

RUN make
