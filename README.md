Using this repo as a reference, you can perform maven filtering in your spring boot application.

What is maven filtering?
Maven plugins have the power to perform powerful tasks for you. One of them is filtering.
Maven filtering simply refers to the resolution of "property values" for your files.
Consider the example below.

Let's say you have a file hello.txt under src/main/resources and contains the following data.
test=@app-title@
hello=@test-heading@

What we want here is for @app-title@ to be replaced by a property "app-title" and for @test-heading@ to be replaced by a property "test-heading".
How can we achieve this?
We can use maven plugins for this.
You can read these properties from 3 possible places.
  1. POM file. (We define them inside the <properties> tag)
  2. Application.properties file
  3. Command-line args

Command - mvn clean package (or) mvn clean install 

Pay special attention to the build section in the POM.
Filtering works out of the box only if you want to read "properties" defined in the <properties> tag inside the POM and wish to refer it in your application properties file or hello.txt file.

But if you also want to read values from you application.properties file and properteis tag, you need to do some changes.

```
<resources>
    <resource>
        <directory>src/main/resources</directory>
        <filtering>true</filtering>
    </resource>
</resources>
```

The above block is used to tell maven for which files you want filtering to be done.

```
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>properties-maven-plugin</artifactId>
    <version>1.0.0</version>
    <executions>
        <execution>
            <phase>initialize</phase>
            <goals>
                <goal>read-project-properties</goal>
            </goals>
            <configuration>
                <files>
                    <file>src/main/resources/application.properties</file>
                </files>
            </configuration>
        </execution>
    </executions>
</plugin>
```

The above tag tells maven to read property values from application.properties file

```
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-resources-plugin</artifactId>
    <version>3.0.2</version>
    <configuration>
        <delimiters>
            <delimiter>@</delimiter>
        </delimiters>
        <useDefaultDelimiters>false</useDefaultDelimiters>
    </configuration>
</plugin>
```

This is the plugin that does the actual replacement.