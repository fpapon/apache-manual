# Apache Manual

Apache Manual is a template project to generate manual documentation of Apache projects.

The goal of this project is to generate the documentation in **html** and **pdf** format using a theme related to the 
[Apache Software Foundation](https://apache.org) website.

This project use the [asciidoctor-maven-plugin](https://github.com/asciidoctor/asciidoctor-maven-plugin).

## Structure

The asciidoc manual example pages are located under `src/manual/asciidoc`.

The example pages is a copy of some of pages of the [Apache Software Foundation](https://apache.org) website.
This pages is used only for the illustration of the usage of this project.

## Generation

### HTML

The custom Apache CSS is located under `src/manual/asciidoc/style/apache.css`.

The images used in the documentation is in the `ìmages` folder.

You have to declare the plugin in the pom.xml of your manual maven module:

```
<profile>
    <id>html</id>
    <build>
        <defaultGoal>process-resources</defaultGoal>
        <plugins>
            <plugin>
                <groupId>org.asciidoctor</groupId>
                <artifactId>asciidoctor-maven-plugin</artifactId>
                <version>1.5.6</version>
                <executions>
                    <execution>
                        <id>output-html</id>
                        <phase>generate-resources</phase>
                        <goals>
                            <goal>process-asciidoc</goal>
                        </goals>
                        <configuration>
                            <backend>html5</backend>
                            <doctype>article</doctype>
                            <attributes>
                                <toc />
                                <linkcss>true</linkcss>
                                <stylesheet>style/apache.css</stylesheet>
                                <imagesdir>images</imagesdir>
                            </attributes>
                        </configuration>
                    </execution>
                </executions>
                <configuration>
                    <sourceDirectory>src/manual/asciidoc</sourceDirectory>
                    <outputDirectory>target/generated-html/${project.version}</outputDirectory>
                    <preserveDirectories>true</preserveDirectories>
                    <headerFooter>true</headerFooter>
                    <imagesDir>src/manual/asciidoc/images</imagesDir>
                </configuration>
            </plugin>
        </plugins>
    </build>
</profile>
```

You can change some configuration parameters like:

***sourceDirectory***

main folder of the asciidoc files.

***outputDirectory***

folder where html files are generated.

For others configuration, you can have a look on the [asciidoctor-maven-plugin](https://github.com/asciidoctor/asciidoctor-maven-plugin).

This example use an `index.adoc` main file and a table of content at the left sidebar. 

To launch the html buidl, just run the maven command using the html profile:

```
mvn clean -Phtml
```

### PDF

The custom Apache theme is located under `src/manual/theme/apache-theme.yml`.

The fonts used is located under `src/manual/theme/fonts`

The images used in the documentation is in the `ìmages` folder.

You have to declare the plugin in the `pom.xml` of your manual maven module:

```
<profile>
    <id>pdf</id>
    <build>
        <defaultGoal>process-resources</defaultGoal>
        <plugins>
            <plugin>
                <groupId>org.asciidoctor</groupId>
                <artifactId>asciidoctor-maven-plugin</artifactId>
                <version>1.5.6</version>
                <dependencies>
                    <dependency>
                        <groupId>org.asciidoctor</groupId>
                        <artifactId>asciidoctorj-pdf</artifactId>
                        <version>1.5.0-alpha.16</version>
                    </dependency>
                </dependencies>
                <configuration>
                    <sourceDirectory>src/manual/asciidoc</sourceDirectory>
                    <outputDirectory>target/generated-pdf/${project.version}</outputDirectory>
                    <preserveDirectories>true</preserveDirectories>
                    <headerFooter>true</headerFooter>
                    <backend>pdf</backend>
                    <attributes>
                        <project-version>${project.version}</project-version>
                        <pdf-stylesdir>${project.basedir}/src/manual/theme</pdf-stylesdir>
                        <pdf-style>apache</pdf-style>
                        <pdf-fontsdir>${project.basedir}/src/manual/theme/fonts</pdf-fontsdir>
                        <imagesdir>images</imagesdir>
                        <icons>font</icons>
                        <pagenums>true</pagenums>
                        <toc/>
                        <idprefix/>
                        <idseparator>-</idseparator>
                        <sectnums>true</sectnums>
                    </attributes>
                </configuration>
                <executions>
                    <execution>
                        <id>generate-pdf-doc</id>
                        <phase>generate-resources</phase>
                        <goals>
                            <goal>process-asciidoc</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    </profile>
```

You can change some configuration parameters like:

***sourceDirectory***

main folder of the asciidoc files.

***outputDirectory***

folder where pdf files are generated.

For others configuration, you can have a look on the [asciidoctor-maven-plugin](https://github.com/asciidoctor/asciidoctor-maven-plugin).

To launch the pdf build, just run the maven command using the *pdf* profile:

```
mvn clean -Ppdf
```

The aggregate generated file is `index.pdf` located in the *outputDirectory*.

## Contribute

If you want to help you are welcome to push some PR or to contact me ;)

Copyright © 2018 The Apache Software Foundation, Licensed under the Apache License, Version 2.0.
Apache and the Apache feather logo are trademarks of The Apache Software Foundation.