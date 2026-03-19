生命周期：实例化、依赖注入、初始化、销毁
1. beanDefinition加载
2. 通过反射实例化bean，依赖注入
3. Aware接口回调
4. BeanPostProcessor（前置方法）
5. 初始化方法
6. BeanPostProcessor（后置方法）
7. Bean可以使用
8. 容易关闭
9. 销毁