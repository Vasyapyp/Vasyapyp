- 👋 Hi, I’m @Vasyapyp
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Vasyapyp/Vasyapyp is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- Project from https://start.vaadin.com/ -->
    <groupId>com.example.application</groupId>
    <artifactId>embedded-jetty</artifactId>
    <name>embedded-jetty</name>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>

    <properties>
        <java.version>17</java.version>
        <maven.compiler.target>${java.version}</maven.compiler.target>
        <maven.compiler.source>${java.version}</maven.compiler.source>

        <vaadin.version>24.0.2</vaadin.version>
        <selenium.version>4.8.1</selenium.version>
    </properties>

    <repositories>
        <repository>
            <id>Vaadin Directory</id>
            <url>https://maven.vaadin.com/vaadin-addons</url>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>
    </repositories>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>com.vaadin</groupId>
                <artifactId>vaadin-bom</artifactId>
                <version>${vaadin.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <dependencies>
        <dependency>
            <groupId>com.vaadin</groupId>
            <!-- Replace artifactId with vaadin-core to use only free components -->
            <artifactId>vaadin</artifactId>
        </dependency>
        <dependency>
            <groupId>org.parttio</groupId>
            <artifactId>line-awesome</artifactId>
            <version>1.1.0</version>
        </dependency>
        <dependency>
            <groupId>jakarta.servlet</groupId>
            <artifactId>jakarta.servlet-api</artifactId>
            <version>5.0.0</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-simple</artifactId>
        </dependency>
        <dependency>
            <groupId>org.eclipse.jetty</groupId>
            <artifactId>jetty-webapp</artifactId>
            <version>11.0.14</version>
        </dependency>
        <dependency>
            <groupId>org.eclipse.jetty.websocket</groupId>
            <artifactId>websocket-jakarta-server</artifactId>
            <version>11.0.14</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>com.vaadin</groupId>
                <artifactId>vaadin-maven-plugin</artifactId>
                <version>${vaadin.version}</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>prepare-frontend</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

    <profiles>
        <profile>
            <!-- Production mode is activated using -Pproduction -->
            <id>production</id>
            <dependencies>
                <!-- Exclude development dependencies from production -->
                <dependency>
                    <groupId>com.vaadin</groupId>
                    <artifactId>vaadin-core</artifactId>
                    <exclusions>
                        <exclusion>
                            <groupId>com.vaadin</groupId>
                            <artifactId>vaadin-dev</artifactId>
                        </exclusion>
                    </exclusions>
                </dependency>
            </dependencies>
            <build>
                <plugins>
                    <plugin>
                        <groupId>com.vaadin</groupId>
                        <artifactId>vaadin-maven-plugin</artifactId>
                        <version>${vaadin.version}</version>
                        <executions>
                            <execution>
                                <goals>
                                    <goal>build-frontend</goal>
                                </goals>
                                <phase>compile</phase>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>

    </profiles>
</project>
