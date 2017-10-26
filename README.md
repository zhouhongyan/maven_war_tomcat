# maven_war_tomcat
maven
springboot  maven打war包部署到tomcat上遇到的问题
pom.xml修改，springboot自带的tomcat冲突，需要增加<exclusions>

<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
			<exclusions>
                <exclusion>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-tomcat</artifactId>
                </exclusion>
             </exclusions>   
		</dependency>
    
    
打的war自动解压到服务器是 mapper.xml文件丢失，<build>需要增加 <resources>
<build>
		<resources>
	      <resource>
	        <directory>src/main/java</directory>
	        <includes>
	          <include>**/*.xml</include>
	        </includes>
	      </resource>
	      <resource>
	        <directory>src/main/resources</directory>
	        <includes>
	          <include>**/*</include>
	        </includes>
	      </resource>
	    </resources>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
