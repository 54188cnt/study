### 设置github代理
socket5：
```bash
git config --global http.https://github.com.proxy socks5://127.0.0.1:51837
```

取消代理：
```bash
git config --global --unset http.proxy git config --global --unset https.proxy
```