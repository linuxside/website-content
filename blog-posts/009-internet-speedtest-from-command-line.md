---
title: Internet speed test from command line
date: 2022-04-07
tags: cli, speed test, network
url: internet-speedtest-from-command-line
---

Run Internet speed test from command line via global server network behind Ookla Speedtest platform.

---

The speed test tool provided by [Ookla Speedtest platform](https://www.speedtest.net/) is a "definitive way to test the speed and performance of your internet connection" with over 16k global servers.

The only requirement is Python. At the moment of writing this note, both Python 2 and Python 3 are supported.

The OS I chose to do this under is Ubuntu 21, but it should work under any Debian derived distribution.

## Installation

There are 2 options to install the `speedtest-cli` tool. One from the [Python Package Index](https://pypi.org/) and another from GitHub repository.

1. Install the latest release from Python Package Index

```bash
sudo pip install speedtest-cli
```

2. Install the latest version from GitHub

```bash
wget -O speedtest-cli https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py
chmod +x speedtest-cli
```

Copy the executable under a path available in the environment variable **$PATH**, so the **speedtest-cli** can be executed without writing its whole path

```bash
sudo mv speedtest-cli /usr/local/bin/speedtest-cli
```

**Note:** the GitHub version will always be greater that the one from [pypi.org](https://pypi.org/project/speedtest-cli/), as it's under active development.

## Usage

1. Simple test

```bash
speedtest-cli --bytes --secure
```

Sample output:

```text
Retrieving speedtest.net configuration...
Testing from Proton AG (194.126.177.64)...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Hosted by HEIG-VD (Yverdon-Les-Bains) [543.81 km]: 1200022.766 ms
Testing download speed................................................................................
Download: 8.77 Mbyte/s
Testing upload speed......................................................................................................
Upload: 4.21 Mbyte/s
```

2. Test the download speed only

```bash
speedtest-cli --bytes --no-upload --secure
```

3. Test the upload speed only

```bash
speedtest-cli --bytes --no-download --secure
```

4. Test via a specific server

List **speedtest.net** servers sorted by distance

```bash
speedtest-cli --list --secure
```

Sample output:

```text
Retrieving speedtest.net configuration...
32777) HHnet (Tabor, Czech Republic) [385.94 km]
17015) JM-Net z.s. (Jesenice, Czech Republic) [429.08 km]
 4162) ISP Alliance a.s. (Prague, Czech Republic) [442.33 km]
34087) ČMIS (Prague, Czech Republic) [442.33 km]
36701) ÚVT internet s.r.o. (Prague, Czech Republic) [442.33 km]
17717) cloudinfrastack, s.r.o. (Prague, Czech Republic) [442.33 km]
30620) O2 Czech Republic, a.s. (Prague, Czech Republic) [442.33 km]
48278) Cloudflare (Prague, Czech Republic) [442.33 km]
 6288) ITBUSINESS s.r.o. (Turnov, Czech Republic) [443.79 km]
17301) AmigoNet s.r.o. (Ústí nad Labem, Czech Republic) [503.06 km]
```

Perform a speed test via a specific server from the list

```bash
speedtest-cli --bytes --secure --server 32777
```

**Resources:**
- [speedtest-cli GitHub repository](https://github.com/sivel/speedtest-cli)
