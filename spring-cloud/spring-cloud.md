### zuul.routes.\*.path 和zuul.routes.\*.serviceId配置之后访问404
1.  诱发原因：zuul配置会默认给context-path加上serviceId(即spring.application.name)
1.  解决方法：zuul.routes.serviceId.strip-prefix=false
