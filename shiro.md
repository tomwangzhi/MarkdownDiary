### shiro概述

1. 几个注解


#### 1. 几个认证注解
1. @RequiresPermissions
2. @RequiresRoles
3. @RequiresUser
4. @RequiresGuest
5. @RequiresAuthentication

> 用在方法上，会有个拦截器在方法执行之前做一些校验判断，判断Subject是不是为null。
  该拦截器是AopAllianceAnnotationsAuthorizingMethodInterceptor
  而实例化是在AuthorizationAttributeSourceAdvisor这个类中new的
  ShiroAnnotationProcessorConfiguration是spring管理的@Configuration 定义了BeanAbstractShiroAnnotationProcessorConfiguration抽象类
  
```text

上面五个注解对应五个方法拦截器:
  RoleAnnotationMethodInterceptor
  PermissionAnnotationMethodInterceptor
  AuthenticatedAnnotationMethodInterceptor
  UserAnnotationMethodInterceptor
  GuestAnnotationMethodInterceptor
  
  均实现MethodInterceptor接口，在方法调用前后调用业务逻辑
   
```   