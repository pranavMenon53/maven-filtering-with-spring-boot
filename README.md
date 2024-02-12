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
