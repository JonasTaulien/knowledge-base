# OpenAPI Generator - Generate Java models only
## Problem
The [Maven plugin for the OpenAPI Generator](https://github.com/OpenAPITools/openapi-generator/tree/master/modules/openapi-generator-maven-plugin)
not only generates model classes but also a full api-client.

But we may want to only generate model classes.

## Solution
We can use the 'java' generator. We then have to disable the generation of everything but the models.
Here is a full example configuration:
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <build>
        <plugins>
            <plugin>
                <groupId>org.openapitools</groupId>
                <artifactId>openapi-generator-maven-plugin</artifactId>
                <executions>
                    <execution>
                        <goals>
                            <goal>generate</goal>
                        </goals>
                        <configuration>
                            <inputSpec>${project.basedir}/src/main/resources/open-api-spec.yaml</inputSpec>
                            <generatorName>java</generatorName>
                            <generateAliasAsModel>false</generateAliasAsModel>
                            <generateApiDocumentation>false</generateApiDocumentation>
                            <generateApis>false</generateApis>
                            <generateApiTests>false</generateApiTests>
                            <generateModelDocumentation>false</generateModelDocumentation>
                            <generateModelTests>false</generateModelTests>
                            <generateSupportingFiles>false</generateSupportingFiles>
                            <!-- This also prefixes all model class-/enum-names with 'Api'-->
                            <modelNamePrefix>Api</modelNamePrefix>
                            <configOptions>
                                <sourceFolder>.</sourceFolder>
                                <dateLibrary>java8</dateLibrary>
                                <java8>true</java8>
                                <modelPackage>com.example.gen.openapi</modelPackage>
                            </configOptions>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

Hint: You may also want to use [a `.openapi-generator-ignore`-File](https://github.com/OpenAPITools/openapi-generator/blob/master/docs/customization.md#ignore-file-format)

[Source](https://github.com/OpenAPITools/openapi-generator/tree/master/modules/openapi-generator-maven-plugin)
