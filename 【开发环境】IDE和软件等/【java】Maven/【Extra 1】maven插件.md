#### 【Extra 1】maven插件

------------------------

* maven-jar-plugin

  ```xml
  <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-jar-plugin</artifactId>
      <version>2.4</version>
      <configuration>
          <source>1.8</source>
          <target>1.8</target>
          <archive>
              <manifest>
                  <mainClass>com.zte.omlmsg.App</mainClass>
                  <addClasspath>true</addClasspath>
                  <classpathPrefix>lib/</classpathPrefix>
              </manifest>
          </archive>
      </configuration>
  </plugin>
  ```

  编译时指定 主类

* maven-enforcer-plugin

  ```xml
  <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-enforcer-plugin</artifactId>
      <version>${maven-enforcer-plugin.version}</version>
      <executions>
          <execution>
              <goals>
                  <goal>enforce</goal>
              </goals>
              <configuration>
                  <rules>
                      <requireMavenVersion>
                          <version>3.6.1</version>
                      </requireMavenVersion>
                  </rules>
                  <fail>true</fail>
              </configuration>
          </execution>
      </executions>
  </plugin>
  ```

  负责制定和检查规则，比如这里指定了 maven的 version

* maven-checkstyle-plugin

  ```xml
  <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-checkstyle-plugin</artifactId>
      <version>${maven-checkstyle-plugin.version}</version>
      <dependencies>
          <dependency>
              <groupId>com.puppycrawl.tools</groupId>
              <artifactId>checkstyle</artifactId>
              <version>${checkstyle.version}</version>
          </dependency>
          <dependency>
              <groupId>com.github.ngeor</groupId>
              <artifactId>checkstyle-rules</artifactId>
              <version>${checkstyle-rules.version}</version>
          </dependency>
      </dependencies>
      <configuration>
          <configLocation>com/github/ngeor/checkstyle.xml</configLocation>
          <includeTestSourceDirectory>true</includeTestSourceDirectory>
          <skip>${skipTests}</skip>
      </configuration>
      <executions>
          <execution>
              <id>checkstyle</id>
              <phase>validate</phase>
              <goals>
                  <goal>check</goal>
              </goals>
          </execution>
      </executions>
  </plugin>
  ```

  使用规范： 如阿里 P3C-PMD规范、华为规范等

* maven-surefire-plugin

  ```xml
  <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-surefire-plugin</artifactId>
      <version>${maven-surefire-plugin.version}</version>
  </plugin>
  ```

  可能是由于历史的原因，Maven 2/3中用于执行测试的插件不是maven-test-plugin，而是maven-surefire-plugin。

* maven-jacoco-plugin

  ```xml
   <plugin>
       <groupId>org.jacoco</groupId>
       <artifactId>jacoco-maven-plugin</artifactId>
       <version>${jacoco-maven-plugin.version}</version>
       <executions>
           <execution>
               <id>pre-unit-test</id>
               <goals>
                   <goal>prepare-agent</goal>
               </goals>
           </execution>
           <execution>
               <id>post-unit-test</id>
               <phase>test</phase>
               <goals>
                   <goal>report</goal>
               </goals>
           </execution>
           <execution>
               <id>check-unit-test</id>
               <phase>test</phase>
               <goals>
                   <goal>check</goal>
               </goals>
               <configuration>
                   <dataFile>${project.build.directory}/jacoco.exec</dataFile>
                   <rules>
                       <rule>
                           <element>BUNDLE</element>
                           <limits>
                               <limit>
                                   <counter>INSTRUCTION</counter>
                                   <value>COVEREDRATIO</value>
                                   <minimum>${jacoco.unit-tests.limit.instruction-ratio}</minimum>
                               </limit>
                               <limit>
                                   <counter>BRANCH</counter>
                                   <value>COVEREDRATIO</value>
                                   <minimum>${jacoco.unit-tests.limit.branch-ratio}</minimum>
                               </limit>
                           </limits>
                       </rule>
                       <rule>
                           <element>CLASS</element>
                           <limits>
                               <limit>
                                   <counter>COMPLEXITY</counter>
                                   <value>TOTALCOUNT</value>
                                   <maximum>${jacoco.unit-tests.limit.class-complexity}</maximum>
                               </limit>
                           </limits>
                       </rule>
                       <rule>
                           <element>METHOD</element>
                           <limits>
                               <limit>
                                   <counter>COMPLEXITY</counter>
                                   <value>TOTALCOUNT</value>
                                   <maximum>${jacoco.unit-tests.limit.method-complexity}</maximum>
                               </limit>
                           </limits>
                       </rule>
                   </rules>
               </configuration>
           </execution>
       </executions>
  </plugin>
  ```

  

