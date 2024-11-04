# CaddyConfig

一个基于[Steamcommunity 302](https://www.dogfight360.com/blog/686/)的Caddy配置，旨在把原删除的功能加回去

**八百年不更新一次警告！！！此仓库处于常年摆烂阶段，作者看不看Issue纯纯看心情，但是看到Issue绝对会尝试帮你解决**

**介意八百年不更新一次的朋友们请异步原版steamcommunity302**

## 如何使用

### 准备文件

**Caddy**  
首先，你需要下载[caddy](https://github.com/caddyserver/caddy/releases/tag/v2.6.2)（目前只在该版本下测试过，勇士可以尝试其他版本。）

下载你的系统的版本
> 如果你是小白不知道下哪个，这里有个不能保证肯定能工作的摘要版本：
Windows: <https://github.com/caddyserver/caddy/releases/download/v2.6.2/caddy_2.6.2_windows_amd64.zip>
Mac老芯片：<https://github.com/caddyserver/caddy/releases/download/v2.6.2/caddy_2.6.2_mac_amd64.tar.gz>
Mac M系列芯片：<https://github.com/caddyserver/caddy/releases/download/v2.6.2/caddy_2.6.2_mac_arm64.tar.gz>
Linux: <https://github.com/caddyserver/caddy/releases/download/v2.6.2/caddy_2.6.2_linux_amd64.tar.gz>

随后解压，得到`caddy.exe`或者`caddy`（取决于你的系统），把它复制出来，到你能找到的地方。

**Steamcommunity 302**  

下载[Steamcommunity 302](https://www.dogfight360.com/blog/686/)（不要纠结这个的版本号，不重要）。  
完成后同样地解压。

**准备Wine或Windows虚拟机**  

（Windows用户请跳过这步）

请自行找教程准备。

**以管理员权限启动`steamcommunity_302.exe`**  

点击`启动服务`按钮，待启动完成后点击`停止 & 退出`按钮。之后在`steamcommunity_302.exe`同目录下你可以发现以下几个文件：

- `steamcommunityCA.pem`
- `steamcommunityCA.key`
- `steamcommunity.key`
- `steamcommunity.crt`

把它们也复制出来，和`caddy.exe`（或者`caddy`）放在一起。

**本仓库**

下载本仓库的以下内容：

- `steamcommunity_302.caddy.json`
- `hosts`

把`steamcommunity_302.caddy.json`和你的`caddy.exe`（或者`caddy`放在一起）。

把`hosts`的所有文件内容复制到你的`hosts`文件中。

## 导入证书

导入`steamcommunityCA.pem`这个根证书。

## 启动

打开你的`caddy.exe`（或者`caddy`）所在文件夹，打开终端，运行：

```
./caddy run --config steamcommunity_302.caddy.json --adapter caddyfile
```

> 给小白的提示：
对于Windows，如何打开终端：
按住键盘上的`Shift`键，右键文件夹空白处，选择`在此处打开PowerShell窗口`。把上面的命令复制粘贴进去，按回车。

## Q&A

- Pixiv（或者某个其他功能）用不了，无法访问怎么办？
steamcommunity302的作者早已移除了pixiv支持，我这个仓库的意义就是给那个功能强行续命，不受作者支持的功能早晚坏掉。挂掉了我也没办法，我也没有学过caddy配置，这仓库只是作为分享。

- Steam客户端登录无限转圈？
用记事本或者其他纯文本编辑器打开`hosts`文件，找到带有`api.steampowered.com`的一行（请善用搜索功能），在该行最前面加一个`#`号，保存。

以下内容搬运自Steamcommunity302的Q&A：（部分内容有删改）  
**该部分更多内容请参见[原页面](https://www.dogfight360.com/blog/686/#:~:text=%E6%AD%A3%E5%B8%B8%E8%AE%BF%E9%97%AEYouTube-,%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E8%A7%A3%E5%86%B3%3A,-%E6%96%87%E4%BB%B6%E8%A2%AB%E5%AE%89%E5%85%A8)**  
- 文件被安全软件自动删除
若为系统自带Windows Defender,遵循以下步骤设置排除项：
运行 windowsdefender:// 或 进入系统设置->手动打开Windows安全中心->病毒和威胁防护->病毒和威胁防护设置->管理设置->排除项->添加或删除排除项。若非系统自带的WD删除,自行进入自己所安装的安全软件添加白名单。
- 出现80/443端口被占用
关闭对应监听端口的进程/服务即可!
可参考该教程排查–>>[传送门](https://www.dogfight360.com/blog/knowledge-base/%e8%a7%a3%e5%86%b3%e5%b8%b8%e8%a7%81%e7%9a%8480-443%e7%ab%af%e5%8f%a3%e8%a2%ab%e5%8d%a0%e7%94%a8%e9%97%ae%e9%a2%98/)
- steam客户端/Chrome/IE提示证书错误
按步骤导入steamcommunityCA.pem到**受信任的根证书发布机构**
若导入证书时提示存储区是只读/存储区已满[请点击查看该链接解决](https://www.dogfight360.com/blog/knowledge-base/%e8%a7%a3%e5%86%b3%e5%af%bc%e5%85%a5%e8%af%81%e4%b9%a6%e6%97%b6%e6%8f%90%e7%a4%ba%e5%ad%98%e5%82%a8%e5%8c%ba%e6%98%af%e5%8f%aa%e8%af%bb-%e5%ad%98%e5%82%a8%e5%8c%ba%e5%b7%b2%e6%bb%a1/)
- Firefox证书错误
访问about:preferences#privacy 拉到最底部
导入时选择证书文件”steamcommunityCA.pem”
