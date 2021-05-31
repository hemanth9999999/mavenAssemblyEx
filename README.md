# mavenAssemblyEx

Inside project tag : 

<build>
		<pluginManagement>
			<plugins>
				<plugin>
			    <artifactId>maven-assembly-plugin</artifactId>
                          <executions>
                                 <execution>
                                       <id>make-assembly</id>
                                       <phase>package</phase>
                                       <goals>
                                              <goal>single</goal>
                                       </goals>
                                       <configuration>
                                       		  <finalName>${project.artifactId}-${project.version}</finalName>
                                              <descriptors>
                                                     <descriptor>assembly/assembly.xml</descriptor>
                                              </descriptors>
                                          
                                       </configuration>
                                 </execution>
                                 <execution>
                                       <id>make-assembly-tar</id>
                                       <phase>package</phase>
                                       <goals>
                                              <goal>single</goal>
                                       </goals>
                                       <configuration>
                                       		  <finalName>${project.artifactId}-${project.version}</finalName>
                                              <descriptors>
                                                     <descriptor>assembly/assembly1.xml</descriptor>
                                              </descriptors>
                                      
                                       </configuration>
                                 </execution>
                          </executions>
			</plugin>
			</plugins>
		</pluginManagement>
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<!-- or whatever current version -->
			</plugin>
			<plugin>
				<groupId>org.scala-tools</groupId>
				<artifactId>maven-scala-plugin</artifactId>
				<version>2.11</version>
				<executions>
					<execution>
						<goals>
							<goal>compile</goal>
							<goal>testCompile</goal>
						</goals>
					</execution>
				</executions>
				<configuration>
					<scalaVersion>${scala.version}</scalaVersion>
				</configuration>
			</plugin>
		</plugins>
	</build>
  
  
  
  assembly.xml
  
  <assembly
	xmlns="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.2"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.2 http://maven.apache.org/xsd/assembly-1.1.2.xsd">
	<id>bin</id>
	<!-- Generates a zip package containing the needed files -->
	<formats>
		<format>zip</format>
	</formats>
	<fileSets>
		<fileSet>
			<directory>script</directory>
			<outputDirectory>script</outputDirectory>
			<includes>
				<include>*.sh</include>
				<include>*.py</include>
			</includes>
			<fileMode>0755</fileMode>
		</fileSet>
		<fileSet>
			<directory>src/main/resources</directory>
			<outputDirectory>resources</outputDirectory>
			<includes>
				<include>*.*</include>
			</includes>
			<fileMode>0755</fileMode>
		</fileSet>
		<fileSet>
			<directory>${project.build.directory}</directory>
			<outputDirectory></outputDirectory>
			<includes>
				<include>*.jar</include>
			</includes>
		</fileSet>
	</fileSets>
</assembly>

assembly1.xml 

<assembly
        xmlns="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.2"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.2 http://maven.apache.org/xsd/assembly-1.1.2.xsd">
        <id>bin</id>
        <formats>
                <format>tar.gz</format>
        </formats>
        	<baseDirectory>../</baseDirectory>
   
    		<includeBaseDirectory>false</includeBaseDirectory>
        <fileSets>
		<!-- Adds startup scripts to the root directory of zip package -->
		
		<fileSet>
			<directory>${project.build.directory}</directory>
			<outputDirectory></outputDirectory>
			<includes>
				<include>*.zip</include>
			</includes>
		</fileSet>
		
		<fileSet>
			<directory>../xlr_install</directory>
			<outputDirectory>xlr_install</outputDirectory>
			<includes>
				<include>*/**</include>
			</includes>
		</fileSet>
	</fileSets>
</assembly>
