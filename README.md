
# SA:MP Reverse Proxy
Used for port forwarding from main VPS (running SAMP) to second VPS. I used this because my main VPS latency is high when connected to PT. TELKOM INDONESIA providers (Indihome, Telkomsel), which my VPS is OVH Singapore, and I thinked of forwarding this OVH VPS to another VPS with lower latency.
## First Step
 - Get frp (fast reverse proxy) from [here](https://github.com/fatedier/frp). Use right build (I'm using amd64).
## Setup in Main VPS
 - Place frpc to your main VPS.
 - Create new file frpc.ini and enter this whole configuration.
```
serverAddr = "SECONDVPSIP"
serverPort = 7000

[[proxies]]
name = "samp"
type = "udp"
localIP = "127.0.0.1"
localPort = yoursampport
remotePort = yourtargetsampport
```
- Save configuration.
## Setup in Second VPS
- Place frps to your second VPS.
- Create new file frps.ini and enter this whole configuration.
```
[common]
bind_port = 7000
```
- Save configuration.
## Running the Reverse Proxy
- In second VPS, run `screen -S frp ./frps`.
- Make sure it's running.
- In main VPS, run `screen -S frp ./frpc`.
- If both is running, you can connect with `yourtargetsampport` before like `SECONDVPSIP:yourtargetsampport`

Red is main VPS and Green is second VPS.
- ![Preview](https://github.com/secretweaponclan/sampreverseproxy/blob/main/preview.PNG?raw=true)
### Small note
Make sure you open OUT/IN connection for port 7000/tcp in both VPS.
