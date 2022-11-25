---
layout：post
title：提示ssh密码的解决
date：2022/11/25 14:05:16.000000000
---
今天突然提示我输入ssh密码  
结果输入哪个密码也不对  
就尝试了重新配置秘钥  
结果还是不行  
提示中显示的还是旧的秘钥  
![](https://img-blog.csdnimg.cn/78a8d3cfc53448cc9166b32a1bb8cad5.png)
后来尝试`ssh -T -p 443 git@ssh.github.com`  
结果也不行  
`The authenticity of host '[ssh.github.com]:443 ([20.205.243.160]:443)' can't be established.`  
提示`Are you sure you want to continue connecting (yes/no)?`     
选择yes
原来是少了一个known_hosts文件，本来密钥文件应该是三个，现在是两个，便报了这样的错误，此时选择yes回车之后，便可，同时生成了缺少了的known_hosts文件：  
![](https://img-blog.csdnimg.cn/20190521101659202.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlYXJsZXNzeG1t,size_16,color_FFFFFF,t_70)  
再 `ssh -T -p 443 git@ssh.github.com`  
终于成功了  
再git push就行了，如果不行可以重新配置秘钥

