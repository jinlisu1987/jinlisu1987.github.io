1. 移除冲突jar包;
2. sdk 担心jar冲突的解决办法:
   将其打包到项目代码里面, 有相关的mvn 插件;
   
   ```
   <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.4.3</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <artifactSet>
                                <includes>
                                    <include>redis.clients:jedis</include>
                                </includes>
                            </artifactSet>
                            <relocations>
                                <relocation>
                                    <pattern>redis.clients</pattern>
                                    <shadedPattern>inner.redis.clients</shadedPattern>
                                </relocation>
                            </relocations>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
   ```
3. 类隔离机制
