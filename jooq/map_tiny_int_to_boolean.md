# jOOQ - Map tiny int to boolean
## Problem
Given the following mysql table:
```mysql
CREATE TABLE my_prefix_user
(
    id                          INT AUTO_INCREMENT PRIMARY KEY,
    acceptedAgbAndPrivacyPolicy BOOLEAN NOT NULL
);
```

When executing jOOQ via `mvn compile`, this will create the following class:
```java
public class MyPrefixUser extends TableImpl<MyPrefixUserRecord> {
    public final TableField<MyPrefixUserRecord, Byte> ACCEPTEDAGBANDPRIVACYPOLICY = ...
}
```

But we want it to generate:
```java
    public final TableField<MyPrefixUserRecord, Boolean> ACCEPTEDAGBANDPRIVACYPOLICY = ...
```

## Solution
In MySQL the type `BOOLEAN` is an alias for `TINYINT(1)`, so we have to create a mapping 
from `(MySQL) tinyint(1)` to `(Java) org.jooq.impl.SQLDataType.BOOLEAN`:
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <build>
        <plugins>
            <plugin>
                <groupId>org.jooq</groupId>
                <artifactId>jooq-codegen-maven</artifactId>
                <configuration>
                    <generator>
                        <database>
                            <name>org.jooq.meta.mysql.MySQLDatabase</name>
                            <forcedTypes>
                                <forcedType>
                                    <name>BOOLEAN</name>
                                    <types>(?i:tinyint)</types>
                                </forcedType>
                            </forcedTypes>
                        </database>
                    </generator>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

[Source](https://blog.jooq.org/2019/09/27/how-to-map-mysqls-tinyint1-to-boolean-in-jooq/)