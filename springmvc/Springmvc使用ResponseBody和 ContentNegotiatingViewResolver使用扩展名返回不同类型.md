1. 第一步配置自己的ContentNegotiationManager替换默认的ContentNegotiationManager

 		<mvc:annotation-driven content-negotiation-manager="contentNegotiationManager">

2. 第二步配置ContentNegotiationManager

        <bean id="contentNegotiationManager" class="org.springframework.web.accept.ContentNegotiationManagerFactoryBean">
        	<!-- 设置为true以忽略对Accept Header的支持-->
            <property name="ignoreAcceptHeader" value="false" />
            <!-- true，开启扩展名支持，false关闭支持 -->  
            <property name="favorPathExtension" value="true"/>
            <!-- 用于开启 /userinfo/123?format=json的支持 --> 
            <property name="favorParameter" value="false" />
            <property name="defaultContentType" value="text/html" />
            <property name="useJaf" value="false"/>
            <property name="mediaTypes">
                <map>
                    <entry key="json" value="application/json" />
                    <entry key="xml" value="application/xml" />
                    <entry key="xls" value="application/vnd.ms-excel" />
                    <entry key="xlsx" value="application/vnd.ms-excel" />
                </map>
            </property>
        </bean>

3. 第三步配置对应的HttpMessageConverter

		<mvc:message-converters>
            <bean class="org.springframework.http.converter.xml.MappingJackson2XmlHttpMessageConverter">
            </bean>
            <bean class="ExcelHttpMessageConverter">
            </bean>
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                <property name="supportedMediaTypes">
                    <list>
                        <value>application/json;charset=UTF-8</value>
                        <value>application/xml;charset=UTF-8</value>
                    </list>
                </property>
            </bean>
        </mvc:message-converters>