这两天被一个奇怪的问题困扰了两天，即@RestController标记下的类里，
@GetMapping标记的方法里，HttpServletRequest request做为传入参数时，
request.getCookies是空的。
<br>
**各种怀疑与排查，**
- 1 Chrome跟踪报文，在请求的Header里带着Cookie，此处没问题；
- 2 怀疑Nginx跨域反向代理配置错误，但反复测试，无效；
- 3 Boot里反复测试，XssFilter关了，ShiroFilter也关了，最后所有Filter全关了，无效；
- 最终发现，并不是没传到后台，而是在request的Header里，Cookie需要从Header里拿，不是直接获取。

<br>
**记下此问题，以防再犯** 