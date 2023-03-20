# how to deploy
以下追記後`mvn deploy`  
`~/.m2/settings.xml`  
```xml
<settings>
  <servers>
    <server>
      <id>github</id>
      <password>GITHUB_TOKEN</password>
    </server>
  </servers>
</settings>
```

`pom.xml`  
```xml
<project>
    <distributionManagement>
        <repository>
            <id>internal.repo</id>
            <name>Temporary Staging Repository</name>
            <url>file://${project.build.directory}/mvn-repo</url>
        </repository>
    </distributionManagement>
    <properties>
        <github.global.server>github</github.global.server>
    </properties>
    <build>
        <plugins>
            <plugin>
                <groupId>com.github.github</groupId>
                <artifactId>site-maven-plugin</artifactId>
                <version>0.12</version>
                <configuration>
                    <message>Maven artifacts for ${project.version}</message>
                    <noJekyll>true</noJekyll>
                    <merge>true</merge>
                    <outputDirectory>${project.build.directory}/master</outputDirectory>
                    <branch>refs/heads/master</branch>
                    <includes><include>**/*</include></includes>
                    <repositoryName>maven</repositoryName>
                    <repositoryOwner>futchiis</repositoryOwner>
                </configuration>
                <executions>
                    <execution>
                        <goals>
                        <goal>site</goal>
                        </goals>
                        <phase>deploy</phase>
                    </execution>
                </executions>
                </plugin>
        </plugins>
   </build>
</project>
```

# How to use
`pom.xml`  
```xml
<project>
  <repositories>
    <repository>
      <id>futchiis</id>
      <name>futchiis repository</name>
      <url>https://raw.githubusercontent.com/futchiis/maven/master</url>
    </repository>
  </repositories>
</project>
```





