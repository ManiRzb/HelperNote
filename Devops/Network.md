# 🛠️ Network Useful Tips

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
