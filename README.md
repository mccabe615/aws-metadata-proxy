你好！
很冒昧用这样的方式来和你沟通，如有打扰请忽略我的提交哈。我是光年实验室（gnlab.com）的HR，在招Golang开发工程师，我们是一个技术型团队，技术氛围非常好。全职和兼职都可以，不过最好是全职，工作地点杭州。
我们公司是做流量增长的，Golang负责开发SAAS平台的应用，我们做的很多应用是全新的，工作非常有挑战也很有意思，是国内很多大厂的顾问。
如果有兴趣的话加我微信：13515810775  ，也可以访问 https://gnlab.com/，联系客服转发给HR。
# AWS Metadata Proxy

Example AWS Metadata proxy to protect against attack vectors targetting AWS Credentials 

## Getting Started

Clone the repo

```
git clone https://github.com/Netflix-Skunkworks/aws-metadata-proxy.git
cd aws-metadata-proxy
```

Build the proxy

```golang
go get
go build
```

## Network Setup

Create an `iptable` rule that prevents talking directly to the AWS Metadata Service **except** for a particular user, `proxy_user` in the example below.  This is the user you run the proxy as on your server.

```
/sbin/iptables -t nat -A OUTPUT -m owner ! --uid-owner proxy_user -d 169.254.169.254 -p tcp -m tcp --dport 80 -j DNAT --to-destination 127.0.0.1:9090
```

