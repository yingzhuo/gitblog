# SpringBoot 配置`servlet`或`filter`

```java
@Configuration
public class ApplicationCnfWeb {

    @Bean
    public FilterRegistrationBean myFilter() {
        FilterRegistrationBean bean = new FilterRegistrationBean();
        bean.addUrlPatterns("/*");
        bean.setFilter(new MyFilter());
        bean.setOrder(Ordered.HIGHEST_PRECEDENCE);
        bean.setName("myFilter");
        return bean;
    }

    @Bean
    public ServletRegistrationBean myServlet() {
        ServletRegistrationBean bean = new ServletRegistrationBean();
        bean.addUrlMappings("/*");
        bean.setName("myServlet");
        bean.setServlet(new MyServlet());
        bean.setOrder(Ordered.HIGHEST_PRECEDENCE);
        return bean;
    }

}
```
