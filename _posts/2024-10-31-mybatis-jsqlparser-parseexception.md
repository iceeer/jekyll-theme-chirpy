---
title: "mybatis报错 net.sf.jsqlparser.parser.ParseException"
date: 2024-10-31 10:50:38 +0800
---

```cobol
Caused by: net.sf.jsqlparser.parser.ParseException: Encountered unexpected token: "with" "WITH"

    at line 4, column 28.

Was expecting one of:

    ","

    ";"

    "CONNECT"

    "CROSS"

    "EXCEPT"

    "FOR"

    "FULL"

    "GROUP"

    "HAVING"

    "INNER"

    "INTERSECT"

    "JOIN"

    "LEFT"

    "MINUS"

    "NATURAL"

    "ORDER"

    "PIVOT"

    "RIGHT"

    "START"

    "UNION"

    "WHERE"

    "WINDOW"

    <EOF>

	at net.sf.jsqlparser.parser.CCJSqlParser.generateParseException(CCJSqlParser.java:20951)

	at net.sf.jsqlparser.parser.CCJSqlParser.jj_consume_token(CCJSqlParser.java:20798)

	at net.sf.jsqlparser.parser.CCJSqlParser.Statements(CCJSqlParser.java:562)

	at net.sf.jsqlparser.parser.CCJSqlParserUtil.parseStatements(CCJSqlParserUtil.java:126)
```

Mapper接口上加上@SqlParser(filter = true)试试

```java
@SqlParser(filter = true)

public interface XxxMapper extends BaseMapper<Xxx> {
```
