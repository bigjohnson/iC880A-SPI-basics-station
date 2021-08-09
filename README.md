# iC880A-SPI-basic-station
How install Semtech Basic Station LoRA packet forwarder on a Raspberry Pi with a Imst iC880A-SPI radio module and connect it to TTN v3

## I wrote this doc for upgrading a working installation on a Raspberry Pi of a Semtech udp packet forwarder to the new Basic Station protocol. If you need to install the hardware go to [the best howto](https://github.com/ttn-zh/ic880a-gateway/wiki) and complete hardware install, stop before software install, and back here.

1. Get the source code:

`git clone https://github.com/lorabasics/basicstation.git`

2. Compile it:

`cd basicstation`

`make platform=rpi variant=std`

2. Manually install it:

`mkdir /opt` if you don't have it on your filesystem

`mkdir /opt/basicstation`

`mkdir /opt/basicstation/bin`

`cp build-rpi-std/bin/station /opt/basicstation/bin`

3. Create config directory:

`mkdir /etc/basicstation`

4. Create the service file:

/lib/systemd/system/basicstation.service

with this content

[Unit]
Description=Basic Sation TTN V3 service

[Service]
WorkingDirectory=/opt/basicstation/bin
ExecStart=/opt/basicstation/bin/station -h /etc/basicstation
SyslogIdentifier=ttn-gateway
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target

