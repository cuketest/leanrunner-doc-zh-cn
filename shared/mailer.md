# 邮件发送

"leanpro.mail"中的**Mailer**类提供了邮件发送的功能。


Mailer类有如下的定义

```javascript

class Mailer {
    /* 获得Mailer类的实例 */
    public static getMailer(mailConfig: MailServerConfig): Mailer;
    
    /* 发送邮件 */
    public sendMail(message: MailMessage): Promise<void>;
}
    
```

其中：

#### getMailer

```javascript
    public static getMailer(mailConfig: MailServerConfig): Mailer;
```

静态方法，传入邮件服务器的配置参数(MailServerConfig)，返回Mailer的实例。这个实例可用来执行后继的邮件发送操作。MailServerConfig有如下的定义：

```javascript

interface MailServerConfig {
    host: string,       //mail server
    port?: number,      //mail server port
    secure: boolean,    //secure connection
    auth: {
        "user": string, //authenticate user
        "pass": string  //password
    }
}

```

当不传port参数时，使用默认的端口25，当不传port参数，且secure=true时，使用默认端口465。

#### sendMail

```javascript
    public sendMail(message: MailMessage): Promise<void>;
```

传入邮件相关参数，发送邮件。
其中MailMessage应有如下的定义：

```
interface MailMessage {
    from: string,    // sender address
    to: string,      // list of receivers
    subject: string, // Subject line
    text: string,    // plain text body
    html: string     // html body
}
```
text是文本格式的内容，html是格式为html的数据

#### 样例

下面是发送邮件的样例：

```javascript
const { Mailer } = require('leanpro.mail');
let mailer = Mailer.getMailer({
    "host": "smtp.domain.com",
    "port": 465,
    "secure": true,
    "auth": {
        "user": "noreply@domain.com",
        "pass": "<mypassword>"
    }
});

(async function () {
    let mailMessage = {
        "from": "noreply@domain.com",
        "to": "someone@domain.com",
        "subject": "test mail",
        "text": 'some test content',
        "html": '<p>some <span style="font-weight:bold">test</span> content</p>',
    };
    await mailer.sendMail(mailMessage);
})();

```

使用需按实际的SMTP服务器信息修改上面的参数。