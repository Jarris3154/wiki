# Maven Java With Dependencies
默认的maven-jar-plugin打jar包的时候没有将maven的依赖打进jar包，这种包只包含了本包中写的class文件，不包括依赖的其他jar包中的class文件，
这种jar包一般是无法运行的。可以在pom.xml中添加以下代码，以支持依赖的打包。

```xml
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-assembly-plugin</artifactId>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <descriptorRefs>
                        <descriptorRef>jar-with-dependencies</descriptorRef>
                    </descriptorRefs>
                    <!--去掉jar-with-dependencies的后缀-->
                    <appendAssemblyId>false</appendAssemblyId>
                </configuration>
            </plugin>
        </plugins>
    </build>
```
