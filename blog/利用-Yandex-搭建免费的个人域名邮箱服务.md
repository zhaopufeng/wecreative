# 利用 Yandex 搭建免费的个人域名邮箱服务
有一个自己的域名邮箱好处多多。你可以用它来重复注册某些网站或服务，如果你在运营网站或播客，还可以用它来和读者、听众们沟通。

自己搭建邮件服务器非常麻烦，你需要解决 TOS、繁琐地搭建、SPF 与 DKIM 的设置等众多问题，更不用提服务器需要自己维护所带来的备份等工作。

随后，我发现 [Yandex](https://www.henduohao.com/tag/yandex-mail "Yandex邮箱 Yandex账号 Yandex邮箱购买") 提供了免费的个性域名服务。和同类型的 QQ 邮箱相比，Yandex 注册过程更简单，不需要手机验证和实名验证，自由度更高。




**Yandex 是什么**

Yandex（俄语：Яндекс）是一家俄罗斯互联网企业，旗下的搜索引擎在俄国内拥有逾 60% 的市场占有率，同时也提供邮箱、网盘等一系列互联网产品和服务。

-   Yandex Mail 的注册入口：[mail.yandex.com](https://mail.yandex.com/) 

<!---->

-   个人域名邮箱申请入口：Connect Yandex




**Yandex 域名邮箱和其它同类服务相比的优势**

-   注册相比自行搭建步骤简单很多
-   由大型企业及服务商维护，无需自行维护
-   免费，并可提供 1000 个自定义前缀邮箱，每个用户 10G 容量

<!---->

-   可以配置 SPF、DKIM，降低被认证为垃圾邮件的几率
-   搭建好后多开邮箱账号无门槛




-   **步骤一：申请和注册**
-   **注册 Yandex 邮箱**

传送门：<https://passport.yandex.com/registration>

![图片描述](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/644bd69bba3e427989de8501db629358~tplv-k3u1fbpfcp-zoom-1.image)\


可以选择用电话号码或者设置安全问题两种方式注册，笔者是使用 [Google Voice](https://www.henduohao.com/tag/google-voice "Google Voice Voice账号 Voice账号购买") 注册的。

### 注册域名邮箱

个人域名邮箱申请入口：[Connect Yandex](https://connect.yandex.com/pdd/)，输入你的顶级域名注册。

![图片描述](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e066e90411fc4fe4a619c24cdc1fa583~tplv-k3u1fbpfcp-zoom-1.image)\


接着就是验证该域名所有权，一共有四种方式：

-   Html files：放一个指定名称的 html 文件到服务器根目录
-   Meta tag：在网站首页加入指定的 meta 头
-   Whois：不推荐，因为大部分的 whois 都被商家做了保护
-   DNS record：在 DNS 解析中加入指定的 TXT 项

对于不懂得网站搭建的朋友，前两种方法注定是行不通了，只能在 DNS 管理后台做 dns 记录。如果你有自己的网站，优先选择方案二，加入一个 meta 头即可。

下面来讲解一下 DNS record 的设置方法，进入 DNS 的后台面板，点击添加 TXT 记录：

Name（host）填写 `yandex-verification`

Value 填写验证页面给定的值，比如 `4b11214ae60a86`

做好验证之后就是等待通过验证的过程，此过程可能短至一天，长至数月，请耐心等待。笔者在今年上半年申请之后没有立即通过，直到最近群友提起才重新拾起查看。

当你点击 [这里](https://connect.yandex.com/portal/import/pdd?from=pdd)，出现如下图显示画面时，说明你已经成功申请域名邮箱：

![图片描述](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/77da3080936b4703b91be5cbcc0900a0~tplv-k3u1fbpfcp-zoom-1.image)

**步骤二：配置 MX、SPF 与 DKIM 记录**

**配置 MX 记录**

进入 DNS 管理后台，找到 mail 设置或者可以填写 MX 记录的地方，Name（Host）填写 `@` 或者你的顶级域名，Value 填写 `mx.yandex.net.`，Priority 填写 `10`。

![图片描述](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f462a17abaf94279839c69581966ea43~tplv-k3u1fbpfcp-zoom-1.image)\


解析好之后静待生效即可。




**配置 SPF 和 DKIM**

SPF 记录有助于降低从域名邮箱发送的电子邮件被标记为垃圾邮件的风险，因此一定要设置。进入 DNS 管理后台，添加新的 TXT 记录。Name（Host）填写 `@` 或者顶级域名，Value 填写 `v = spf1 redirect = _spf.yandex.net`。更具体的操作可以参考官网：[传送门](https://yandex.com/support/domain/set-mail/spf.html)

使用 DKIM 签名，电子邮件收件人可以验证邮件是否真的来自所谓的发件人。进入 DNS 管理后台，添加新的 TXT 记录。Name（Host）填写 `mail._domainkey`，Value 填写 Yandex.Connect 设置中复制的「公钥」中的文本块。

-   公钥获取地址：[传送门](https://connect.yandex.com/portal/admin/customization/mail)

<!---->

-   更具体的操作可以参考官网：[传送门](https://yandex.com/support/connect/dns/dkim.html?form-org_id=2765523&form-v=0)

<!---->

-   ![图片描述](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8ec9a65c000144ef92d9615daafbf2cd~tplv-k3u1fbpfcp-zoom-1.image)\

-   解析好之后静待生效即可。
-   

-   **步骤三：自定义域名邮箱前缀**

如果你完成了以上所有步骤并且通过了 Yandex 的官方验证，那么恭喜你，你已经有了属于自己的域名邮箱。下面要做的工作就是通过简单的设置自定义域名邮箱的前缀。

进入 [这里](https://connect.yandex.com/portal/admin/departments/1)（Все сотрудники），点击「Add」添加一位用户，并完成域名前缀和密码的设置。




![图片描述](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0a011d3868b34b82a8ebeea414a45671~tplv-k3u1fbpfcp-zoom-1.image)\


创建好之后回到 [Yandex mail 官网](https://mail.yandex.com/) 登录，用户名和密码填写刚刚创建的信息即可。切记一定要登录，因为这里有一个协议需要同意，同意后该自定义前缀的域名邮箱方可开通。

Enjoy it！

**\
**

**补充内容**

配置中，如果你需要用到这些资讯，可以参考

-   POP3：pop.yandex.com SSL 端口：995
-   SMTP：smtp.yandex.com SSL 端口：465
-   IMAP：imap.yandex.com SSL 端口：993
-   API：<https://tech.yandex.com/domain/doc/about-docpage/>

<!---->

-   DNS record 全指南：\


<!---->

-   
    ![图片描述](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bb54e06114a34a969e261190885ef121~tplv-k3u1fbpfcp-zoom-1.image)

本文链接：[https://www.henduohao.com/a/yandex-mail-register-method](https://www.henduohao.com/a/yandex-mail-register-method "利用 Yandex 搭建免费的个人域名邮箱服务")，转载请注明出处，谢谢！