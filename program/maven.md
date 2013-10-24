# set main class

	<build>
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-jar-plugin</artifactId>
				<configuration>
					<archive>
						<manifest>
							<mainClass>com.maventest.App</mainClass>
						</manifest>
					</archive>
				</configuration>
			</plugin>
		</plugins>
	</build>

# make source jar
http://maven.apache.org/plugin-developers/cookbook/attach-source-javadoc-artifacts.html
```xml
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-source-plugin</artifactId>
<executions>
<execution>
<id>attach-sources</id>
<goals>
<goal>jar</goal>
</goals>
</execution>
</executions>
</plugin>
```
javadoc:
```xml
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-javadoc-plugin</artifactId>
<executions>
<execution>
<id>attach-javadocs</id>
<goals>
<goal>jar</goal>
</goals>
</execution>
</executions>
</plugin>
```
# mvn depending on a Native or JNI library
https://www.darkcornersoftware.com/confluence/display/MAVEN/Depending+on+a+Native+or+JNI+Library

# mvn clear cache
Sometimes the maven repository is changed, for example the url for that resource is different, but the cached repository will still using the cached setting.xml which is located in the ~/.m2/ directory. 
To solve the problem delete the ~/.m2/* to focre maven to reload the stuff.

