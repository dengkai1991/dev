# **Spring启动之BeanPostProcessor后置处理器**

## **相关的BeanPostProcessor类图**
![类结构图](https://images.effiu.cn/blog/spring/BeanPostProcessor.png)
![类结构图2](https://images.effiu.cn/blog/spring/BeanPostProcessor_class.jpg)


## **BeanPostProcessor作用**

排序后的BeanPostProcessor顺序为:

1. ApplicationContextAwareProcessor
2. ConfigurationClassPostProcessor.ImportAwareBeanPostProcessor
3. PostProcessorRegistrationDelegate.BeanPostProcessorChecker
4. CommonAnnotationBeanPostProcessor
5. AutowiredAnnotationBeanPostProcessor
6. ApplicationListenerDetector

## **InstantiationAwareBeanPostProcessor解析**
```
    //实例化之后的处理
    default boolean postProcessAfterInstantiation(Object bean, String beanName) throws BeansException {
        return true;
    }
    //实例化之前的处理
    @Nullable
    default Object postProcessBeforeInstantiation(Class<?> beanClass, String beanName) throws BeansException {
        return null;
    }
    //修改属性值
    @Nullable
    default PropertyValues postProcessProperties(PropertyValues pvs, Object bean, String beanName)
            throws BeansException {
        return null;
    }
```

postProcessProperties 方法运行的时机 ，主要是 在 填充属性的时候， 就是 AbstractAutowireCapableBeanFactory#populateBean 这个里面 调用的， 主要是在填充属性之前 再进行相关的操作。

InstantiationAwareBeanPostProcessor # postProcessProperties 方法被实现的了也比较多， 这里主要讲两个 ：

1. CommonAnnotationBeanPostProcessor ： 主要 注册带有 @Resource 注解的 属性
2. AutowiredAnnotationBeanPostProcessor ： 主要解决 带有 @Autowired，@Value，@Lookup，@Inject 注解的属性

InstantiationAwareBeanPostProcessor 主要是 在实例化前后作一些增强性的操作，是在 AbstractAutowireCapableBeanFactory#createBean 里面创建之前被触发调用的 ， 而 postProcessProperties 方法是在 填充属性的时候，对一些 注解式属性 进行注入.
