# 🛠️ Network Useful Tips



### 🧭 Table of Contents

1. [🚀 Simple and Fast Port Forwarding with `socat`](#-simple-and-fast-port-forwarding-with-socat)
2. [🚀 Quick FTP Server with `pyftpdlib`](#-quick-ftp-server-with-pyftpdlib-no-setup-required)
3. [🚀 One-Liner HTTP File Server](#-one-liner-http-file-server-no-setup)
4. [🚀 Transfer Files Over SSH](#-transfer-files-over-ssh-no-scp-needed)
5. [🚀 SSH Port Forwarding (Local Tunnel)](#-create-a-secure-tunnel-with-ssh-port-forwarding)
6. [🚀 Reverse SSH Tunnel (Bypass NAT)](#-reverse-ssh-tunnel-access-a-remote-machine-behind-nat)
7. [🚀 Check Open Ports with `nc`](#-check-open-ports-on-a-host)
8. [🚀 Test a Port with `nc`](#-test-a-port-is-open-and-accepting-connections)
9. [🚀 Mirror TCP Traffic with `socat`](#-mirror-traffic-tcp-between-two-hosts)
10. [🚀 Find Local IP Address](#-find-your-local-ip-address-quickly)
---

## 🚀 Simple and Fast Port Forwarding with `socat`

Forward incoming traffic on one port to another host and port with a single command:

```bash
socat TCP-LISTEN:4128,fork TCP:192.168.1.142:3128
```

> This forwards all traffic received on local port `4128` to the remote host `192.168.1.142` on port `3128`.

* `TCP-LISTEN:4128` — Listen on local port `4128`
* `fork` — Allow multiple simultaneous connections
* `TCP:192.168.1.142:3128` — Target destination for forwarding

---

## 🚀 Quick FTP Server with `pyftpdlib` (No Setup Required)

Spin up a simple FTP server instantly using Python:

```bash
python -m pyftpdlib -p 2121 -w -d "/tmp/myftp"
```

> This starts an FTP server on port `2121`, with write access enabled, serving the folder `/tmp/myftp`.

#### 📄 Available Options:

| Option           | Description                           |
| ---------------- | ------------------------------------- |
| `-p <port>`      | Set port to listen on (default: `21`) |
| `-w`             | Enable write access (upload, delete)  |
| `-d <folder>`    | Set the root directory to serve       |
| `-u <username>`  | Require login with this username      |
| `-P <password>`  | Require login with this password      |
| `-i <ip>`        | Bind server to a specific IP address  |
| `-r <start-end>` | Set passive mode port range           |
| `-v`             | Enable verbose logging                |
| `--help`         | Show full command-line help           |


📝 **Tip**: If you only need anonymous access (no user/pass), just omit `-u` and `-P`.

---
## 🚀 One-Liner HTTP File Server (No Setup)
Share files over HTTP instantly:

```bash
python3 -m http.server 8080 --directory /tmp/myfiles
```
> Serves the contents of `/tmp/myfiles` on port `8080` via HTTP. Open in browser: `http://<your-ip>:8080`

---

## 🚀 Transfer Files Over SSH (No SCP Needed)

Send a file to another machine using raw SSH + `cat`:

```bash
cat myfile.txt | ssh user@remote 'cat > ~/myfile.txt'
```

> Super quick way to transfer files over SSH without `scp`.

---

## 🚀 Create a Secure Tunnel with SSH Port Forwarding

Forward a remote port to your local machine:

```bash
ssh -L 8080:localhost:3000 user@remote-host
```

> Access remote port `3000` through your local `localhost:8080`.

---

## 🚀 Reverse SSH Tunnel (Access a Remote Machine Behind NAT)

Expose a service running on a remote device (like IoT/Pi):

```bash
ssh -R 9000:localhost:22 user@your-server.com
```

> Now connect to the remote machine from the server using:
> `ssh -p 9000 user@localhost`

---

## 🚀 Check Open Ports on a Host

Quick TCP port scan using `nc` (netcat):

```bash
nc -zv 192.168.1.1 20-1000
```

> Scans ports `20` to `1000` on host `192.168.1.1` and shows which are open.

---

## 🚀 Test a Port Is Open and Accepting Connections

```bash
nc -v 192.168.1.100 22
```

> Check if port `22` (SSH) is open on `192.168.1.100`.

---

## 🚀 Mirror Traffic (TCP) Between Two Hosts

Use `socat` as a TCP proxy:

```bash
socat TCP-LISTEN:9000,fork TCP:remote-server:80
```

> Acts like a proxy: connect to your local `9000`, it tunnels to `remote-server:80`.

---

## 🚀 Find Your Local IP Address Quickly

```bash
ip a | grep inet
```

> Shows IPs of all interfaces. Or:

```bash
hostname -I
```
---
