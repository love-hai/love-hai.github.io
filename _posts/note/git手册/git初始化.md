### 下载git以及连接github

#### 设置本地用户

这个不是登录，而是给你的电脑设置一个用户，上传的时候，告诉远程仓库是谁上传的。
`git config --global user.name "love-hai"`（双引号不用删，里面内容替换掉）
`git config --global user.email "xiahaifeng2000@gmail.com"`

#### 生成公共密钥

这个密钥是放在仓库里来生产私钥的

`ssh-keygen -t rsa -C `"xiahaifeng2000@gmail.com"

new ：

```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
```


C:\Users\\admin\\.ssh里面，admin指的是用户名。
找到id_rsa.pub文件，复制粘贴全部内容（一行很长的字符串）

#### Github上验证

登录github ->进入设置->SSH and GPG key ->新建密钥
把上面文件里的内容全部复制粘贴进去即可。

#### 验证是否成功

在Git Bash里输入 `ssh -T git@github.com` ，成功的话会出现
You’ve successfully authenticated, but GitHub does not provide shell access.。
初次设置有个Yes同意一下即可。

### 配置代理

#### 找到自己的代理端口

一般来说是在使用的vpn上就能找到

#### 设置代理

git config --global https.proxy http://127.0.0.1:`<port>`
git config --global http.proxy https://127.0.0.1:`<port>`

#### 取消代理

git config --global --unset http.proxy
git config --global --unset https.proxy
