# SSH and SCP Through a Proxy Server with ProxyJump

## Overview

This document provides instructions for using SSH (Secure Shell) and SCP (Secure Copy Protocol) through a proxy server using the ProxyJump option. This method is applicable for OpenSSH versions 7.4p1-11 or later. 

ProxyJump simplifies the process of connecting to a destination server via an intermediate (proxy) server. It is especially useful in scenarios where direct access to the destination server is restricted.

## Prerequisites

- OpenSSH 7.4p1-11 or later installed on your local machine.
- Access credentials for the proxy server and the destination server.
- Network connectivity to both the proxy server and the destination server.

## Using SSH with ProxyJump

To connect to a destination server via a proxy server using SSH, use the following syntax:

```bash
ssh -J <User>@<Proxy-Server> <User>@<Destination-Server>
```

### Example

To connect to `192.168.10.100` via the proxy server `10.23.100.70`, you would use:

```bash
ssh -J user@10.23.100.70 user@192.168.10.100
```

After executing this command, you will first be prompted for the password of the proxy server (`user@10.23.100.70`), followed by the password for the destination server (`user@192.168.10.100`).

## Using SCP with ProxyJump

To transfer files to a destination server via a proxy server using SCP, the command syntax is as follows:

```bash
scp -o "ProxyJump <User>@<Proxy-Server>" <File-Name> <User>@<Destination-Server>:<Destination-Path>
```

### Example

To copy `dataFile.txt` to `/tmp` on `192.168.10.100` via the proxy server `10.23.100.70`, the command is:

```bash
scp -o "ProxyJump user@10.23.100.70" dataFile.txt user@192.168.10.100:/tmp
```

Enter the password for the proxy server (`user@10.23.100.70`) and the destination server (`user@192.168.10.100`) when prompted. The file transfer progress will be displayed, concluding with the file size and transfer speed upon completion.

## Conclusion

Using the ProxyJump option with SSH and SCP offers a streamlined method to access and transfer files to servers across networks where direct access might not be possible. Ensure that you have the necessary permissions and that your OpenSSH version supports ProxyJump.

---

For more information, visit [OpenSSH Documentation](https://www.golinuxcloud.com/ssh-proxy/)


This README.md file provides a basic guide to using SSH and SCP through a proxy server, making it easier for users to connect to servers and transfer files securely.
