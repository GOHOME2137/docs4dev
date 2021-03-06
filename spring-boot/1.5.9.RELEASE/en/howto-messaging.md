## 86. Messaging

Spring Boot offers a number of starters that include messaging. This section answers questions that arise from using messaging with Spring Boot.

## 86.1 Disable Transacted JMS Session

If your JMS broker does not support transacted sessions, you have to disable the support of transactions altogether. If you create your own  `JmsListenerContainerFactory` , there is nothing to do, since, by default it cannot be transacted. If you want to use the  `DefaultJmsListenerContainerFactoryConfigurer`  to reuse Spring Boot’s default, you can disable transacted sessions, as follows:

```java
@Bean
public DefaultJmsListenerContainerFactory jmsListenerContainerFactory(
		ConnectionFactory connectionFactory,
		DefaultJmsListenerContainerFactoryConfigurer configurer) {
	DefaultJmsListenerContainerFactory listenerFactory =
			new DefaultJmsListenerContainerFactory();
	configurer.configure(listenerFactory, connectionFactory);
	listenerFactory.setTransactionManager(null);
	listenerFactory.setSessionTransacted(false);
	return listenerFactory;
}
```

The preceding example overrides the default factory, and it should be applied to any other factory that your application defines, if any.

