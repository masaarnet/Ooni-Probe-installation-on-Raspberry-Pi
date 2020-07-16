# Install old version of Ooni Probe on Raspberry Pi

This instruction is only  to install the [old version of Ooni Probe](https://pypi.org/project/ooniprobe/2.3.0/) on Raspberry Pi. This version of Ooni Probe has been discontinued.
Now, OONI’s team is developing new version based on Go programming language. This version is still not fully operational on Raspberry Pi. You can[ read more here.](https://github.com/ooni/probe)

**Thanks to the ["Icarus" project](https://github.com/icaruslab) ♡**

# Installation

This instruction was tested on:

-  Raspberry Pi 4
- Raspberry Pi OS (32-bit) Lite (Minimal image based on Debian Buster)

## Setup

To install old version of Ooni Probe you will need the following dependencies:

`python``python-dev``python-setuptools``build-essential``libdumbnet1``python-dumbnet``python-libpcap``tor``libgeoip-dev``libpcap0.8-dev``libssl-dev``libffi-dev``libdumbnet-dev`

On Raspberry Pi OS (32-bit) Lite (Minimal image based on Debian Buster) this can generally be done by running:

`sudo apt-get install python python-pip libpcap-dev libgeoip-dev libdnet-dev libdumbnet-dev python-dev libffi-dev libssl-dev libxml2-dev libxslt1-dev libjpeg8-dev zlib1g-dev -y`

When you got them run:

`sudo pip install ooniprobe`

Then, Run:

`sudo apt-get install  software-properties-common tor torsocks obfs4proxy -y`

Now, Run Ooni Probe test:

` ooniprobe web_connectivity --url http://torproject.org/`

**Note:** The software will ask you some questions. Choose to upload the measurements via Onion

Then, restart Tor:

`sudo systemctl restart tor`

**the last step**

Edit ooniprobe.conf file:

`sudo nano /var/lib/ooni/ooniprobe.conf`

Remove `#` before `socks_port` and change it to: `9050`

`socks_port: 9050`

## Examples of usage

Run the web_connectivity test on http://torproject.org:

`ooniprobe web_connectivity --url http://torproject.org/`

Run the http_invalid_request_line test to detect middleboxes:

`ooniprobe http_invalid_request_line`

Run the http_header_field_manipulation test to detect middleboxes:

`ooniprobe http_header_field_manipulation`

List all the available tests:

`ooniprobe -s`
