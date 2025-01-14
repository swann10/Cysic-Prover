# Cysic-Prover Guide Tutorial

Tutor Prover CYSIC : 
1. Regist Cysic https://testnet.cysic.xyz (https://testnet.cysic.xyz/m/referral/invite?code=367ab) or code 367ab

2. Buy GPU Cloud at vast.ai with minimum spesification cpu 32, ram 200, 1x 3060 or 4090, Deposit with stripe or coinbase 

3. Generate key ssh di moba xterm
Guide here: https://github.com/aidilfahmi/Testnet/blob/main/Tutorials/vast.ai.md

4. Setting up Prover (0x-Fill with your address)

```bash
curl -L github.com/cysic-labs/phase2_libs/releases/download/v1.0.0/setup_prover.sh > ~/setup_prover.sh && bash ~/setup_prover.sh 0x-Fill-in-your-reward-address-here"
```

```bash
cd
sha256sum cysic-prover/*.so cysic-prover/prover"
```

```bash
cd
mkdir -p cysic-prover/~/.cysic/assets/scroll/v1/params
mkdir -p .scroll_prover/params
curl -L --retry 999 -C - circuit-release.s3.us-west-2.amazonaws.com/setup/params20 -o .scroll_prover/params/params20
curl -L --retry 999 -C - circuit-release.s3.us-west-2.amazonaws.com/setup/params24 -o .scroll_prover/params/params24
curl -L --retry 999 -C - circuit-release.s3.us-west-2.amazonaws.com/setup/params25 -o .scroll_prover/params/params25
cp .scroll_prover/params/* cysic-prover/~/.cysic/assets/scroll/v1/params/
sha256sum .scroll_prover/params/*"
```

```bash
apt install -y supervisor
```

```bash
echo '[unix_http_server]
file=/tmp/supervisor.sock   ; the path to the socket file

[supervisord]
logfile=/tmp/supervisord.log ; main log file; default $CWD/supervisord.log
logfile_maxbytes=50MB        ; max main logfile bytes b4 rotation; default 50MB
logfile_backups=10           ; # of main logfile backups; 0 means none, default 10
loglevel=info                ; log level; default info; others: debug,warn,trace
pidfile=/tmp/supervisord.pid ; supervisord pidfile; default supervisord.pid
nodaemon=false               ; start in foreground if true; default false
silent=false                 ; no logs to stdout if true; default false
minfds=1024                  ; min. avail startup file descriptors; default 1024
minprocs=200                 ; min. avail process descriptors;default 200
strip_ansi=true

[rpcinterface:supervisor]
supervisor.rpcinterface_factory=supervisor.rpcinterface:make_main_rpcinterface

[supervisorctl]
serverurl=unix:///tmp/supervisor.sock ; use a unix:// URL  for a unix socket

[program:cysic-prover]
command=/root/cysic-prover/prover
numprocs=1
directory=/root/cysic-prover
priority=999
autostart=true
redirect_stderr=true
stdout_logfile=/root/cysic-prover/cysic-prover.log
stdout_logfile_maxbytes=1GB
stdout_logfile_backups=1
environment=LD_LIBRARY_PATH="/root/cysic-prover",CHAIN_ID="534352"' > supervisord.conf
supervisord -c supervisord.conf
```

- Cek Logs
```bash
supervisorctl tail -f cysic-prover
```

- Backup keys in /root/cysic-prover/~/.cysic/assets/ 
