> 提醒： 滥用可能导致账户被BAN！！！   
  
* 使用v2ray+caddy同时部署通过ws传输的vmess vless trojan shadowsocks socks等协议  
* 支持tor网络，且可通过自定义网络配置文件启动v2ray和caddy来按需配置各种功能  
* 支持存储自定义文件,目录及账号密码均为AUUID,客户端务必使用TLS连接  
  
[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/asswedrdf/wdljdxy)  
### 客户端
* **务必替换所有的appname.herokuapp.com为heroku分配的项目域名**  
* **务必替换所有的d0b5b2ba-6aff-4d3f-9c5d-b3a27106581d为部署时设置的AUUID**  
  
<details>
<summary>v2ray</summary>

```bash
* 客户端下载：https://github.com/v2fly/v2ray-core/releases
* 代理协议：vless 或 vmess
* 地址：appname.herokuapp.com
* 端口：443
* 默认UUID：d0b5b2ba-6aff-4d3f-9c5d-b3a27106581d
* 加密：none
* 传输协议：ws
* 伪装类型：none
* 路径：/d0b5b2ba-6aff-4d3f-9c5d-b3a27106581d-vless // 默认vless使用/$uuid-vless，vmess使用/$uuid-vmess
* 底层传输安全：tls
```
</details>
  
<details>
<summary>trojan-go</summary>

```bash
* 客户端下载: https://github.com/p4gefau1t/trojan-go/releases
{
    "run_type": "client",
    "local_addr": "127.0.0.1",
    "local_port": 1080,
    "remote_addr": "appname.herokuapp.com",
    "remote_port": 443,
    "password": [
        "d0b5b2ba-6aff-4d3f-9c5d-b3a27106581d"
    ],
    "websocket": {
        "enabled": true,
        "path": "/d0b5b2ba-6aff-4d3f-9c5d-b3a27106581d-trojan",
        "host": "appname.herokuapp.com"
    }
}
```
</details>
  
<details>
<summary>shadowsocks</summary>

```bash
* 客户端下载：https://github.com/shadowsocks/shadowsocks-windows/releases/
* 服务器地址: appname.herokuapp.com
* 端口: 443
* 密码：password
* 加密：chacha20-ietf-poly1305
* 插件程序：v2ray-plugin_windows_amd64.exe  //需将插件https://github.com/shadowsocks/v2ray-plugin/releases下载解压后放至shadowsocks同目录
* 插件选项: tls;host=appname.herokuapp.com;path=/d0b5b2ba-6aff-4d3f-9c5d-b3a27106581d-ss
```
</details>
  
<details>
<summary>cloudflare workers example</summary>

```js
const SingleDay = 'appname.herokuapp.com'
const DoubleDay = 'appname.herokuapp.com'
addEventListener(
    "fetch",event => {
    
        let nd = new Date();
        if (nd.getDate()%2) {
            host = SingleDay
        } else {
            host = DoubleDay
        }
        
        let url=new URL(event.request.url);
        url.hostname=host;
        let request=new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```
</details>
  
> [更多来自热心网友PR的使用教程](/tutorial)
