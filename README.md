[![Public Domain Unlicense][license-shield]][license-url]

<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/linsomniac/ztproxy">
  </a>

  <h3 align="center">ZTProxy</h3>

  <p align="center">
    A user-space proxy from stdin/stdout to a TCP port on a ZeroTier network
    using Python 3 and libzt.
  </p>
</p>

## Overview

Like "netcat", but for talking to ZeroTier endpoints.

My initial use case is as a SSH ProxyCommand to connect from a Docker
container on my CI/CD service (which not configured to allow tun/tap
devices), to a deploy server reachable over ZeroTier.


### Built With

* [libzt](https://github.com/zerotier/libzt)
* [Python 3](https://www.python.org/)



## Getting Started

### Prerequisites

You will need a ZeroTier network VPN/Overlay.  You can
[register for a ZeroTier network](https://my.zerotier.com/), they are free for
smaller networks.  This is shockingly easy to set up.  You will need the network
ID for the command-line below.

Use pip to install "libzt" wrappers for Python.


### Installation

1. Clone the repo
   ```sh
   git clone https://github.com/linsomniac/ztproxy
   ```
2. Install "libzt" Python module
  ```sh
  pip3 install libzt
  ```
3. For SSH usage, add a line similar to the following in your 
  "~/.ssh/config" file:
  ```
  Host zthost
     ProxyCommand /usr/bin/python3 /path/to/ztproxy /tmp 1234567890abcdef 9994 10.3.2.1 22
  ```

Once the above is done, you can then `ssh user@zthost`.  If the ZeroTier
network is "Private", you will need to use the ZeroTier Central web UI
to allow the new client connection.


## Usage

The command line usage is:

  ```
  /usr/bin/python3 /path/to/ztproxy [IDENTITY_DIR] [NETWORK_ID] [NETWORK_PORT] [ZT_REMOTE_ADDR] [PORT]
  ```

The arguments are as follows:

1. `IDENTITY_DIR` - This is a directory for storing identity files for
    the ZeroTier node endpoint.  It can be "." for testing or ephemeral
    use cases like in a Docker container.  These identity files are
    created by ztproxy.  If you want to make multiple connections and
    preserve the ztproxy IP (and the allow in the ZeroTier Central
    UI for a Private network endpoint), make a directory for storing
    the identities.
2. `NETWORK_ID` - This is the ZeroTier network ID in hex, as found in the
    ZeroTier Central UI.
3. `NETWORK_PORT` - I don't know exactly how to find this, I've been using 9994
    and it has been working.
4. `ZT_REMOTE_ADDR` - The ZeroTier IP address (found in the ZeroTier Central web
    UI) of the host to connect to.
5. `PORT` - The TCP port on the remote host to connect to.  For example, port 22
    for SSH.


<!-- LICENSE -->
## License

Distributed under the Public Domain Unlicense. See `LICENSE.txt` for more information.


## Contact

Project Link: [https://github.com/linsomniac/ztproxy](https://github.com/linsomniac/ztproxy)


<!-- ACKNOWLEDGEMENTS
## Acknowledgements

* []()
* []()
* []()
-->

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[license-shield]: https://img.shields.io/github/license/linsomniac/ztproxy.svg?style=for-the-badge
[license-url]: https://github.com/linsomniac/ztproxy/blob/main/LICENSE.txt
[Public Domain Unlicense](https://choosealicense.com/licenses/unlicense/)
