# Install old version of Ooni Probe on Raspberry Pi

This instruction is only  to install the [old version of Ooni Probe](https://pypi.org/project/ooniprobe/2.3.0/) on Raspberry Pi. This version of Ooni Probe has been discontinued.
Now, OONI’s team is developing new version based on Go programming language. This version is still not fully operational on Raspberry Pi. You can[ read more here.](https://github.com/ooni/probe)

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

`apt-get install  software-properties-common tor torsocks obfs4proxy -y`

Now, Run Ooni Probe test:

` ooniprobe web_connectivity --url http://torproject.org/`

**Note:** The software will ask you some questions. Choose to upload the measurements via Onion

Then, Run:

`sed -i '$ a UseBridges 1\nClientTransportPlugin obfs4 exec /usr/bin/obfs4proxy\nBridge obfs4 173.198.253.234:5638 21C1BF910F9B593D516F05A3ADFAAE57C568A4EC cert=7s2edg1/nSJ/mZbzoS70Kgwe6TfIwezU1mUXQZS7HGGehTTNo2rMUPgkrxFBd22Thpb0WQ iat-mode=0\nBridge obfs4 81.89.100.154:8080 0497E3F325C6853792158A9E28978B1E9F094312 cert=vmxzm+tQMrG1WzQuHCjzofqIE2zTaHEKMMS+gc4R3UzLyJLDrJPobJnJVWc/E46hke3MVg iat-mode=0\nBridge obfs4 172.104.136.81:9200 03FA71574D2EDF101A65BC313A401094792FB1DE cert=A8xCSmf6ByBb1kWCH+HQm9/B8pAvaaHbatNj0tUJenETWm0Z9un0XzLSv7yCiBwMxaO1SA iat-mode=0\nBridge obfs4 79.136.160.201:46501 66AC975BF7CB429D057AE07FC0312C57D61BAEC1 cert=dCtn9Ya8z+R8YQikdWgC3XTAt58z5Apnm95QHrJwnhFSdnphPPEz+NMm6OawWc2srKLjJg iat-mode=0\nBridge obfs4 38.229.33.149:33746 DA18B8A29BD4ADAF0EEDC89C5390A1664BB6E203 cert=ZGbhRaNiQTUWMn2hFqCzgd6dc+KqnTPFxJMhe7MP/yLoJJ1vlWxswpDtRLQDPSgqJB3RcA iat-mode=1' /etc/tor/torrc`

Then, restart Tor:

`restart tor`

**the last step**

Edit ooniprobe.conf file:

`nano /var/lib/ooni/ooniprobe.conf`

Remove `#` before `socks_port` and change it to: `9050`

`tor:``socks_port: 9050`

## Examples of usage

Run the web_connectivity test on http://torproject.org:

`ooniprobe web_connectivity --url http://torproject.org/`

Run the http_invalid_request_line test to detect middleboxes:

`ooniprobe http_invalid_request_line`

Run the http_header_field_manipulation test to detect middleboxes:

`ooniprobe http_header_field_manipulation`

List all the available tests:

`ooniprobe -s`
