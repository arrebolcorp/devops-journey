# Networking and SSH on a cloud server

**Date:** Sat, Nov 21, 2026
**Goal:** connect to a DigitalOcean droplet with an SSH key, run my own `system-report.sh` on it, and destroy the droplet.
**Why it matters for a DevOps cloud job:** every cloud job starts with reaching servers securely, troubleshooting uses IPs, DNS, ports and firewalls, and destroying what you do not use controls cost.


## 1. Pre-flight (Step 0)
| # | Command or action | Function | Concept and use | What I saw (real output) | Screenshot (ss) |
|---|---|---|---|---|---|
| 0.1 | Billing, Spend alerts tab | Confirms a spend alert exists | Cost control: you are warned before the bill grows | | ss-00a (hide email) |
| 0.2 | Droplets list | Confirms there are no old droplets | A clean account has no forgotten resources that bill | | ss-00b |

## 2. Networking in my VM (Step 1)
| # | Command or action | Function | Concept and use | What I saw (real output) | Screenshot (ss) |
|---|---|---|---|---|---|
| 1.1 | `ip -br a` | Lists network interfaces and their IPs in short form | Interface, loopback `lo` (127.0.0.1), private IP. Use it to know your machine's addresses | | ss-01 |
| 1.2 | `ip route` | Shows the routing table | The `default via` line is the gateway, where traffic leaves your network | | ss-02 |
| 1.3 | `ping -c 3 1.1.1.1` | Sends 3 test packets to an IP | Tests connectivity without DNS. `-c 3` means three packets | | ss-03 |
| 1.4 | `getent hosts cloudflare.com` | Resolves a name to an IP | DNS turns names into IP addresses | | ss-04 |
| 1.5 | `curl -4 -s ifconfig.me` | Prints my public IPv4 address | NAT: my VM has a private IP, the internet sees my public IP | | ss-05 (hide public IP) |

## 3. SSH key pair (Step 2)
| # | Command or action | Function | Concept and use | What I saw (real output) | Screenshot (ss) |
|---|---|---|---|---|---|
| 2.1 | `ssh-keygen -t ed25519 -C "ubuntu-lab"` | Creates a key pair. `-t` is the key type, `-C` is a comment | Public-key authentication is safer than passwords. The passphrase protects the private key | | ss-06 (never type the passphrase in a screenshot) |
| 2.2 | `ls -l ~/.ssh` | Lists the key files with permissions | Private key `-rw-------` (600), public key `-rw-r--r--` (644). SSH checks these permissions | | ss-07 |
| 2.3 | `cat ~/.ssh/id_ed25519.pub` | Prints the public key | The public key is the one I upload to the server. Never print or share `id_ed25519` | | ss-08 (optional, public key only) |

## 4. Droplet creation (Step 3)
| # | Command or action | Function | Concept and use | What I saw (real output) | Screenshot (ss) |
|---|---|---|---|---|---|
| 3.1 | DigitalOcean, Security, Add SSH Key | Uploads my public key, named `ubuntu-lab` | The server will accept the matching private key | | ss-09 |
| 3.2 | Create, Droplets | Creates the server: New York or San Francisco, latest Ubuntu LTS, Basic cheapest plan, SSH key, extras off, hostname `s2-ssh-lab` | A droplet is a cloud virtual machine billed by the hour | | ss-10 (hide IP) |
| 3.3 | Copy the public IP | Gets the address to connect to | Servers are reached by their public IP | | ss-11 (hide IP) |
| 3.4 | `DROPLET_IP="..."` (if I used it) | Stores the IP in a variable | Variables avoid retyping the IP and avoid typing the placeholder `<DROPLET_IP>` | | no screenshot needed |

## 5. Connect and explore the server (Step 4)
| # | Command or action | Function | Concept and use | What I saw (real output) | Screenshot (ss) |
|---|---|---|---|---|---|
| 4.1 | `ssh root@$DROPLET_IP` | Opens a remote shell as user `root` | SSH connects to port 22 of a server | | ss-12 (hide IP) |
| 4.2 | Answer `yes` at the first connection | Saves the server fingerprint in `known_hosts` | Host verification protects against a fake server | | included in ss-12 |
| 4.3 | `whoami` | Prints the current user | Confirms I am `root` on the server | | ss-13 |
| 4.4 | `hostname` | Prints the machine name | Confirms I am on `s2-ssh-lab`, not on my VM | | ss-13 |
| 4.5 | `head -2 /etc/os-release` | Shows the first 2 lines of the OS information | Confirms the operating system of the server | | ss-13 |
| 4.6 | `ip -br a` | Shows the server interfaces | The public IP sits on `eth0` | | ss-14 (hide IP) |
| 4.7 | `ss -tln` | Lists listening TCP ports, numeric. `-t` TCP, `-l` listening, `-n` numbers | Port 22 is where SSH listens | | ss-15 |
| 4.8 | `ping -c 3 1.1.1.1` | Tests connectivity from the cloud | The server reaches the internet | | ss-16 |
| 4.9 | `getent hosts cloudflare.com` | Tests DNS from the cloud | The server resolves names | | ss-16 |

## 6. Firewall with ufw (Step 5)
| # | Command or action | Function | Concept and use | What I saw (real output) | Screenshot (ss) |
|---|---|---|---|---|---|
| 5.1 | `ufw status` | Shows the firewall state | A firewall is a set of rules that allows or blocks traffic. Starts `inactive` | | ss-17 |
| 5.2 | `ufw allow OpenSSH` | Adds a rule that allows SSH (port 22) | Always allow SSH first | | ss-18 |
| 5.3 | `ufw enable` (answer `y`) | Turns the firewall on | Enabling it without an SSH rule would lock me out | | ss-18 |
| 5.4 | `ufw status` | Confirms `active` and the OpenSSH rule | Verify before closing the session | | ss-19 |
| 5.5 | `exit` | Closes the SSH session | Returns to my VM | | no screenshot needed |

## 7. Key permissions (Step 6)
| # | Command or action | Function | Concept and use | What I saw (real output) | Screenshot (ss) |
|---|---|---|---|---|---|
| 6.1 | `chmod 644 ~/.ssh/id_ed25519` | Makes the private key readable by group and others | Too open: this is what SSH does not accept | | ss-20 |
| 6.2 | `ssh root@$DROPLET_IP` (or with `-o IdentitiesOnly=yes -i ~/.ssh/id_ed25519`) | Tries to connect | SSH fails with `UNPROTECTED PRIVATE KEY FILE` and `Permissions 0644 ... are too open` | | ss-21 (hide IP) |
| 6.3 | `chmod 600 ~/.ssh/id_ed25519` | Only the owner can read and write | Least privilege: the private key belongs to one user | | ss-22 |
| 6.4 | `ssh root@$DROPLET_IP` | Connects again | It works because the permissions are correct | | ss-22 (hide IP) |
| 6.5 | `exit` | Closes the session | | | no screenshot needed |

## 8. My script on the server (Step 7)
| # | Command or action | Function | Concept and use | What I saw (real output) | Screenshot (ss) |
|---|---|---|---|---|---|
| 7.1 | `ls ~/devops-lab/week2-lab/scripts/system-report.sh` | Checks the file exists locally | Check before copying | | ss-23 |
| 7.2 | `scp ~/devops-lab/week2-lab/scripts/system-report.sh root@$DROPLET_IP:~/` | Copies the file to the server home folder over SSH | `scp` uses SSH, so it needs the same key | | ss-24 (hide IP) |
| 7.3 | `ssh root@$DROPLET_IP` | Connects to the server | | | ss-24 |
| 7.4 | `chmod u+x system-report.sh` | Gives the owner permission to execute | A copied file needs the execute bit | | ss-25 |
| 7.5 | `./system-report.sh` | Runs my script on the server | My script works in the cloud. The "Largest folders" section is empty because `~/devops-lab` does not exist there | | ss-25 |
| 7.6 | `cat system-report-*.txt` | Prints the report | `*` matches any characters in the file name | | ss-26 |
| 7.7 | `exit` | Closes the session | | | no screenshot needed |

## 9. Destroy the droplet (Step 8)
| # | Command or action | Function | Concept and use | What I saw (real output) | Screenshot (ss) |
|---|---|---|---|---|---|
| 8.1 | Droplets, menu, Destroy, confirm | Deletes the droplet | Only destroying stops the billing. Powering off does not | | ss-27 |
| 8.2 | Check Droplets, Volumes, Snapshots, Reserved IPs | Confirms nothing else is left | Forgotten resources keep billing | | ss-28 |
| 8.3 | Empty Droplets list | Evidence that the cloud is clean | Evidence for the portfolio and the interview | | ss-29 |
| 8.4 | `ls -l ~/.ssh` | Final check of my key permissions | Private key must be `-rw-------` | | ss-30 |

## 10. Concepts I learned
| Concept | Short definition (rewrite in my words) | Where I used it |
|---|---|---|
| IP address | The address of a device on a network | `ip -br a`, `ssh root@IP` |
| Private and public IP | Private works inside a network, public is what the internet sees | `ip -br a`, `curl ifconfig.me` |
| NAT | Lets many private IPs share one public IP | `curl ifconfig.me` |
| Gateway | The router where traffic leaves my network | `ip route` |
| DNS | Turns a name into an IP address | `getent hosts` |
| Port | A number that identifies a service on a machine, for example 22 for SSH | `ss -tln` |
| SSH | A secure way to open a shell on a remote server | `ssh root@IP` |
| Key pair | A private key that stays secret and a public key I share | `ssh-keygen` |
| Fingerprint and `known_hosts` | The server's identity, saved the first time I connect | answering `yes` |
| Firewall and `ufw` | Rules that allow or block traffic | `ufw allow OpenSSH` |
| `scp` | Copies files over SSH | Step 7 |
| Permission 600 | Only the owner can read and write | `chmod 600` on the private key |
| Billing by hour | The droplet costs while it exists, even powered off | Destroy at the end |




## 11. Quiz (answer in my own words)
1. What does NAT do, and what is the difference between a private IP and a public IP?

   My answer:

2. What does DNS do? Which command showed it?

   My answer:

3. In an SSH key pair, which part is shared and which stays secret?

   My answer:

4. Why did SSH refuse the key with permissions 644?

   My answer:

5. Why destroy the droplet instead of powering it off?

   My answer:

Bonus
6. What does typing `yes` at the first connection do?

   My answer:

7. Why must I allow SSH before running `ufw enable`?

   My answer:

8. What happened with `<DROPLET_IP>` or the SSH agent, and what did I learn?

   My answer:


