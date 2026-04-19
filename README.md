# netchecker

**Simple network health checker with JSON configuration**

`netchecker` is a lightweight CLI tool that checks the availability of hosts across multiple networks using ICMP (ping). It is designed to be simple, fast, and easily configurable via a JSON file.

---

## ✨ Features

* 🔍 Check multiple networks in a single run
* 📄 JSON-based configuration
* ⚠️ Support for **critical** and **non-critical** hosts
* 🎯 Filter specific networks
* 📊 Clean, readable CLI output with summaries
* ⚡ Fast execution (single ping per host)
* 🧩 Perfect for homelabs, monitoring scripts, and quick diagnostics

---

## 📦 Installation

### Arch Linux (AUR)

```bash
yay -S netchecker
```

Or development version:

```bash
yay -S netchecker-git
```

---

### Manual

```bash
git clone https://github.com/radlesner/netchecker.git
cd netchecker
chmod +x netchecker
sudo install -Dm755 netchecker /usr/bin/netchecker
```

---

## 🚀 Usage

```bash
netchecker [OPTIONS]
```

### Options

| Option         | Description                                          |
| -------------- | ---------------------------------------------------- |
| `-f <file>`    | Path to JSON config file                             |
| `-n <network>` | Filter specific network (can be used multiple times) |
| `-l`           | List available networks                              |
| `-h`           | Show help                                            |

---

## 📂 Configuration

Default config location:

```bash
~/.config/netchecker/hosts.json
```

If the file does not exist, it will be created automatically.

---

## 🧾 Config format

```json
{
  "networks": [
    {
      "network": "network-01.local",
      "hosts": [
        {
          "name": "Router #1",
          "ip": "192.168.0.1",
          "mode": "critical"
        },
        {
          "name": "Host #1",
          "ip": "192.168.0.101",
          "mode": "noncritical"
        }
      ]
    },
    {
      "network": "network-02.local",
      "hosts": [
        {
          "name": "Router #2",
          "ip": "192.168.1.1",
          "mode": "critical"
        },
        {
          "name": "Host #2",
          "ip": "192.168.1.101",
          "mode": "noncritical"
        }
      ]
    }
  ]
}
```

### Modes

* **critical** → failure affects network status
* **noncritical** → failure is reported but does not break network

---

## 📋 Examples

### Check all networks

```bash
netchecker
```

### Use custom config

```bash
netchecker -f network.json
```

### Check specific network

```bash
netchecker -n network-01.local
```

### Check multiple networks

```bash
netchecker -n network-01.local -n network-02.local
```

### List available networks

```bash
netchecker -l
```

---

## 📊 Example output

```
[ℹ] Checking network-01.local network
[✓] RTR-01                  192.168.1.1      0.7 ms    reachable
[✓] NAS                     192.168.1.10     1.2 ms    reachable
[ℹ] SUMMARY: draga.local
[✓] reachable               2
[▲] failed non-critical     0
[✗] failed                  0

[ℹ] ------------------------------------------------------------------------
[ℹ] SUMMARY NETWORK STATUS
[✓] draga.local             OK
```

---

## ❗ Exit codes

| Code | Meaning                       |
| ---- | ----------------------------- |
| `0`  | All networks operational      |
| `1`  | At least one failure detected |

---

## 🧠 Use cases

* 🏠 Homelab monitoring
* 🌐 VPN / multi-site connectivity checks
* ⚙️ Pre-deployment checks
* 🔧 Quick troubleshooting
* 🧪 Lab environments

---

## 🛠 Dependencies

* `bash`
* `jq`
* `iputils`

---

## 📄 License

GPL-3.0

---

## 🤝 Contributing

Feel free to open issues or submit pull requests.

---

## ⭐ Tips

* Use with cron for periodic checks
* Combine with `notify-send` or scripts for alerts
* Integrate into monitoring pipelines

---

## 📌 Author

Created by radlesner
