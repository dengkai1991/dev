# **Gi操作**

## 1. **代理配置**
 * git config --global https.proxy http://127.0.0.1:1080
 * git config --global https.proxy https://127.0.0.1:1080
 * git config --global --unset http.proxy
 * git config --global --unset https.proxy

### **指定域名设置代理：**
* git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
* git config --global https.https://github.com.proxy socks5://127.0.0.1:1080

### **查看config配置信息**
 * git config --global --list

