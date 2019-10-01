# jOOQ - Map tiny int to boolean
```xml
<generator>
    <database>
        <forcedTypes>
            <forcedType>
                <name>BOOLEAN</name>
                <types>(?i:tinyint)</types>
            </forcedType>
        </forcedTypes>
    </database>
</generator>
```

[Source](https://blog.jooq.org/2019/09/27/how-to-map-mysqls-tinyint1-to-boolean-in-jooq/)