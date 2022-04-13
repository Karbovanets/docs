# How to run Karbo node as Linux service

On this page you will find description how to run karbowanecd with JSON PRC as Linux service that will restart itself if daemon crashes for some reason. This example is for Ubuntu server 18.04 x64, but it can be applied to any of the linux versions with small changes.

## Create Linux service to start karbowanecd

1. To start service we will use user _karbo_, so lets create it, manage permissions and login:
```
useradd -m -s /bin/bash -G adm,systemd-journal,sudo karbo && passwd karbo
groupadd karbo
usermod -a -G karbo karbo
su karbo
```

2. Create directory _/KARBO/_ in home directory of _karbo_ user:
```
cd ~
mkdir KARBO
cd KARBO
```

3. Download latest Linux version of Karbo and unpack it:

This one is for Linux 18.04, if you have other version, find a corresponding release at https://github.com/seredat/karbowanec/releases/
```
wget https://github.com/seredat/karbowanec/releases/download/v.1.7.6/Karbo-cli-ubuntu18.04-v.1.7.6.tar.gz
tar -xvzf Karbo-cli-ubuntu18.04-v.1.7.6.tar.gz
rm Karbo-cli-ubuntu18.04-v.1.7.6.tar.gz
```

4. Create log file and add permision to write it:
```
sudo touch /var/log/karbowanecd
sudo chgrp -R karbo /var/log/karbowanecd
sudo chmod -R 770 /var/log/karbowanecd
```

5. Optionally you can pre-download blockchain bootstrap to speed-up process:
```
cd KARBO
mkdir .karbowanec
cd .karbowanec
wget https://bootstrap.karbo.io/blockchain-$(date "+%Y-%m-%d").tar.gz
tar -xvzf blockchain-$(date "+%Y-%m-%d").tar.gz
rm -f blockchain-$(date "+%Y-%m-%d").tar.gz
```

Exit to `root`
```
exit
```

6. Add Karbo to firewall:
```
apt-get install ufw -y
ufw default allow outgoing
ufw default deny incoming
ufw allow ssh/tcp
ufw limit ssh/tcp
ufw allow http/tcp
ufw allow https/tcp
ufw allow 32348/tcp comment "KARBO"
ufw logging on
ufw -f enable
systemctl enable ufw
ufw status
```

Retun to `karbo`
```
su karbo
cd ~
```

7. Lets check if everything is ok. Try to run daemon with _karbo_ user permission and wait for SYNCHRONIZED OK.
Do not forget to change address to your wallet!
```
sudo -u karbo KARBO/karbowanecd --data-dir=KARBO/.karbowanec --log-file=/var/log/karbowanecd --restricted-rpc --enable-cors=* --enable-blockchain-indexes --rpc-bind-ip=0.0.0.0 --rpc-bind-port=32348 --fee-address=KixW1oDMYMyabY6CdwS13fQuUwmUeXTPThF9s9JfDggbXSQGnZXkrP9LvcJtV9x7qb2pLsSobkXWXCrPsGGeC1V6VPBhPva --fee-amount=0.1
```
After that, stop it via entering `exit` inside daemon session.

If you facing errors, you could run Karbo node with debug:
```
sudo -u karbo KARBO/karbowanecd --data-dir=KARBO/.karbowanec --log-file=/var/log/karbowanecd --restricted-rpc --enable-cors=*  --enable-blockchain-indexes --rpc-bind-ip=0.0.0.0 --rpc-bind-port=32348 --log-level=4 --fee-address=KixW1oDMYMyabY6CdwS13fQuUwmUeXTPThF9s9JfDggbXSQGnZXkrP9LvcJtV9x7qb2pLsSobkXWXCrPsGGeC1V6VPBhPva --fee-amount=0.1
```

Exit to `root`
```
exit
```

8. To autostart _karbowanecd_ daemon, we need to create service file in _/etc/systemd/system_:
```
sudo nano /etc/systemd/system/karbowanecd.service
```

```
[Unit]
Description=karbowanecd
Documentation=http://karbo.io
After=syslog.target

[Service]
User=karbo
Restart=always
RestartSec=10
ExecStart=/home/karbo/KARBO/karbowanecd --data-dir=/home/karbo/KARBO/.karbowanec --log-file=/var/log/karbowanecd --restricted-rpc --enable-cors=*  --enable-blockchain-indexes --rpc-bind-ip=0.0.0.0 --rpc-bind-port=32348 --fee-address=KixW1oDMYMyabY6CdwS13fQuUwmUeXTPThF9s9JfDggbXSQGnZXkrP9LvcJtV9x7qb2pLsSobkXWXCrPsGGeC1V6VPBhPva --fee-amount=0.1
StandardInput=tty-force
TTYVHangup=yes
TTYPath=/dev/tty20
#TTYReset=yes
#RemainAfterExit=false
SuccessExitStatus=143

[Install]
WantedBy=multi-user.target
```

**Do not forget to change address to your wallet!**

9. Run service:
```
systemctl daemon-reload
systemctl enable karbowanecd.service
systemctl start karbowanecd.service
```

10. Check service status:
```
karbo@karbonode.top:~/KARBO$ sudo systemctl status karbowanecd.service
● karbowanecd.service - karbowanecd
   Loaded: loaded (/etc/systemd/system/karbowanecd.service; enabled; vendor preset: enabled)
   Active: active (running) since Sat 2020-10-17 19:24:47 CEST; 5s ago
     Docs: http://karbo.io
 Main PID: 5368 (karbowanecd)
    Tasks: 1 (limit: 4915)
   CGroup: /system.slice/karbowanecd.service
           └─5368 /home/karbo/KARBO/karbowanecd --data-dir=/home/karbo/KARBO/.karbowanec --log-file=/var/log/karbowanecd --restricted-rpc --

Oct 17 19:24:47 karbonode.top systemd[1]: Started karbowanecd.
lines 1-10/10 (END)
```

And check your Karbo masternode from browser:  
(don't forget to change server url to yours)
- http://karbonode.top:32348/feeaddress
- http://karbonode.top:32348/getinfo

You should see something like
```
{
  "fee_address": "KixW1oDMYMyabY6CdwS13fQuUwmUeXTPThF9s9JfDggbXSQGnZXkrP9LvcJtV9x7qb2pLsSobkXWXCrPsGGeC1V6VPBhPva",
  "fee_amount": 100000000000,
  "status": "OK"
}
```
and
```
{
  "already_generated_coins": "8741526.871278777480",
  "alt_blocks_count": 0,
  "block_major_version": 4,
  "contact": "",
  "cumulative_difficulty": 4061326490174723,
  "difficulty": 11531062982,
  "grey_peerlist_size": 3737,
  "height": 543420,
  "incoming_connections_count": 0,
  "last_known_block_index": 543419,
  "max_cumulative_block_size": 1423487,
  "min_fee": 100000000000,
  "next_reward": 4800694002995,
  "outgoing_connections_count": 5,
  "rpc_connections_count": 4,
  "start_time": 1602955812,
  "status": "OK",
  "top_block_hash": "50dff3d81e48b90168e0015009660587a17a396282d28011aad71c27f1488b65",
  "transactions_count": 619557,
  "transactions_pool_size": 5,
  "version": "1.7.6.957-6070815b",
  "white_peerlist_size": 268
}
```

You can connect to the node's output by `sudo conspy 20 #` if you install _conspy_.

## Update Karbo node
1. Login to _karbo_ user, go to 'KARBO' folder: 
```
su karbo
cd KARBO
```
2. Check current Karbo version: `./karbowanecd --version`
3. wget new Karbo binaries from https://github.com/seredat/karbowanec/releases/.
4. Stop Karbo daemon: `sudo systemctl stop karbowanecd.service`
5. Extract Karbo binaries and replace old with a fresh one.
6. Start Karbo daemon: `sudo systemctl start karbowanecd.service` and check Karbo daemon status `sudo systemctl status karbowanecd.service` and version: `./karbowanecd --version`