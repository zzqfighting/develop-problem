### zuul.routes.\*.path 和zuul.routes.\*.serviceId配置之后访问404
#####诱发原因：zuul配置会默认给context-path加上serviceId(即spring.application.name)
#####解决方法：zuul.routes.serviceId.strip-prefix=false

### feign.FeignException: status 401 reading
#####诱发原因1：远程调用了一个需要认证的接口
#####解决办法1：自定义一个config：
public class FeignConfig implements RequestInterceptor {
    @Override
    public void apply(RequestTemplate requestTemplate) {
        Map<String, String> requestMap = getHeaders(getHttpServletRequest());
        requestMap.forEach((k, v) -> requestTemplate.header(k, v));
    }

    private HttpServletRequest getHttpServletRequest() {
        try {
            return ((ServletRequestAttributes) RequestContextHolder.getRequestAttributes()).getRequest();
        } catch (Exception e) {
            return null;
        }
    }

    private Map<String, String> getHeaders(HttpServletRequest request) {
        Map<String, String> map = new LinkedHashMap<>();
        Enumeration<String> enumeration = request.getHeaderNames();
        while (enumeration.hasMoreElements()) {
            String key = enumeration.nextElement();
            String value = request.getHeader(key);
            map.put(key, value);
        }
        return map;
    }
}
并在接口中加上：
@FeignClient(name = "${xxx.application.name}",configuration = FeignConfig.class)
public interface RelationFeign {
}

#####在加了configuration还出现
#####诱发原因2：对同一个FeignClient创建了两个以上的实例
#####解决办法2：统一为一个FeignClient创建一个实例，或是所有实例均加上configuration