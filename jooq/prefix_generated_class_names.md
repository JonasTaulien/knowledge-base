# jOOQ - Prefix generated class names
## Problem
It's common that we prefix tables in a sql database:
```sql
CREATE TABLE my_prefix_user
(
    id    INT AUTO_INCREMENT PRIMARY KEY,
    type  ENUM('ADMIN', 'CUSTOMER') NOT NULL
);
```

When executing jOOQ via `mvn compile`, this will create the following classes:
* `enums/MyPrefixUserType`
* `tables/MyPrefixUser`
* `tables/records/MyPrefixUserRecord`

and a table identifier named `tables.MyPrefixUser.MY_PREFIX_USER`.

But we may want to remove the prefix from the generated class-/enum names and from the 
generated table identifiers.

## Solution
We can add a 'matcher strategy':
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <build>
        <plugins>
            <plugin>
                <groupId>org.jooq</groupId>
                <artifactId>jooq-codegen-maven</artifactId>
                <configuration>
                    <generator>
                        <strategy>
                            <matchers>
                                <tables>
                                    <table>
                                        <!-- Match all tables starting with 'my_prefix' -->
                                        <expression>^my_prefix_(.*)$</expression>

                                        <tableClass>
                                            <!-- Name all table classes 'Db$1Table' (e.g DbUserTable) -->
                                            <expression>db_$1_table</expression>
                                            <transform>PASCAL</transform>
                                        </tableClass>

                                        <tableIdentifier>
                                            <!-- Name all table identifiers '$1' (uppercase) (e.g. USER) -->
                                            <expression>$1</expression>
                                            <transform>UPPER</transform>
                                        </tableIdentifier>

                                        <recordClass>
                                            <!-- Name all record classes 'Db$1' (e.g. DbUser) -->
                                            <expression>db_$1</expression>
                                            <transform>PASCAL</transform>
                                        </recordClass>
                                    </table>
                                </tables>

                                <enums>
                                    <enum>
                                        <!-- Match all enums starting with 'my_prefix' -->
                                        <expression>^my_prefix_(.*)$</expression>
                                        <enumClass>
                                            <!-- Name all enums 'Db$1' (e.g. DbUserType) -->
                                            <expression>db_$1</expression>
                                            <transform>PASCAL</transform>
                                        </enumClass>
                                    </enum>
                                </enums>
                            </matchers>
                        </strategy>
                    </generator>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

Now, when executing jOOQ via `mvn compile`, this will create the following classes:
* `enums/DbUserType`
* `tables/DbUserTable`
* `tables/records/DbUser`

and a table identifier named `tables.DbUserTable.USER`.

[Source](https://www.jooq.org/doc/latest/manual/code-generation/codegen-matcherstrategy/)