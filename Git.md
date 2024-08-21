### Git clone 时出现 gnutls_handshake() faile

``` shell
fatal: unable to access 'https://github.com/agilexrobotics/mobile_aloha_sim.git/': 
gnutls_handshake() failed: The TLS connection was non-properly terminated.
```

https://blog.csdn.net/yiyongjiang/article/details/121498080

将 git 链接中的 https 改为 http 即可
``` shell
# git clone https://github.com/agilexrobotics/mobile_aloha_sim.git
git clone http://github.com/agilexrobotics/mobile_aloha_sim.git
```

### Github Proxy
https://mirror.ghproxy.com/

在 Github url 前加上 `https://mirror.ghproxy.com/` 即可
``` shell
git clone https://mirror.ghproxy.com/https://github.com/Yifan-Song793/ETO.git
```
