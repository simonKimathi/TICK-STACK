TICK STACK

Telegraf

Pull the container
docker pull telegraf
Initializes sample config
docker run -v $PWD/telegraf.conf:/etc/telegraf/telegraf.conf:ro telegraf

Run the docker image
docker run -d --name=telegraf \
--net=influxdb \
-v /var/run/docker.sock:/var/run/docker.sock \
-v $PWD/telegraf.conf:/etc/telegraf/telegraf.conf:ro \
telegraf
Supported Locations
docker run -d --name=telegraf \
-v $PWD/telegraf.conf:/etc/telegraf/telegraf.conf:ro \
-v /:/hostfs:ro \
-e HOST_ETC=/hostfs/etc \
-e HOST_PROC=/hostfs/proc \
-e HOST_SYS=/hostfs/sys \
-e HOST_VAR=/hostfs/var \
-e HOST_RUN=/hostfs/run \
-e HOST_MOUNT_PREFIX=/hostfs \
telegraf
Output for telegraf.conf
[[inputs.cpu]]
[[outputs.file]]

Mine run

docker run -d --name telegraf --net=influxdb -v /home/symoh/workspace/docker-images/telegraf/telegraf.conf:/etc/telegraf/telegraf.conf:ro telegraf


Influxdb2
Pull docker
docker pull influxdb

Create config
docker run --rm influxdb:2.0 influxd print-config > config.yml

Run image
docker run -p 8086:8086 \
-v $PWD/config.yml:/etc/influxdb2/config.yml \
Influxdb:2.0
Create network
docker network create influxdb

EG mine
docker run -d --name influxdb2 --net=influxdb -p 8086:8086  -v /home/symoh/workspace/docker-images/TICK-STACK/influxdb2/config.yml:/etc/influxdb2/config.yml influxdb:2.0






Chronograf
Pull image
docker pull chronograf

Create influxdb network and start influxdb container with the same
docker network create influxdb

start
docker run -p 8888:8888 \
--net=influxdb \
chronograf --influxdb-url=http://influxdb:8086
Eg mine
docker run -d --name chronograf -p 8888:8888  --net=influxdb  chronograf --influxdb-url=http://influxdb:8086

Kapacitor
Pull image
docker pull kapacitor
Sample config
docker run --rm kapacitor kapacitord config > kapacitor.conf
run
docker run -p 9092:9092 \
-v $PWD/kapacitor.conf:/etc/kapacitor/kapacitor.conf:ro \
kapacitor

Eg
docker run -d -p 9092:9092  -v /home/symoh/workspace/docker-images/TICK-STACK/kapacitor/kapacitor.conf:/etc/kapacitor/kapacitor.conf:ro       kapacitor
