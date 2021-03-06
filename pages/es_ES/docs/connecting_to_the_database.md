---
title: Connecting to database
layout: page
---
## Conexión a la base de datos

Para conectarse a una base de datos, necesita importar primero el controlador de la base de datos. Por ejemplo:

```go
import _ "github.com/go-sql-driver/mysql"
```

GORM ha envuelto algunos controladores, para que sea más fácil recordar su ruta de importación, por lo que podría importar el controlador de mysql con

```go
import _ "github.com/jinzhu/gorm/dialects/mysql" // import _ "github.com/jinzhu/gorm/dialects/postgres" // import _ "github.com/jinzhu/gorm/dialects/sqlite" // import _ "github.com/jinzhu/gorm/dialects/mssql"
```

## Bases de Datos Compatibles

### MySQL

**NOTE:**

In order to handle `time.Time` correctly, you need to include `parseTime` as a parameter. ([More supported parameters](https://github.com/go-sql-driver/mysql#parameters))

In order to fully support UTF-8 encoding, you need to change `charset=utf8` to `charset=utf8mb4`. See this [article](https://mathiasbynens.be/notes/mysql-utf8mb4) for a detailed explanation.

```go
import (   "github.com/jinzhu/gorm"   _ "github.com/jinzhu/gorm/dialects/mysql" ) func main() {   db, err := gorm.Open("mysql", "user:password@/dbname?charset=utf8&parseTime=True&loc=Local")   defer db.Close() }
```

### PostgreSQL

```go
import (   "github.com/jinzhu/gorm"   _ "github.com/jinzhu/gorm/dialects/postgres" ) func main() {   db, err := gorm.Open("postgres", "host=myhost port=myport user=gorm dbname=gorm password=mypassword")   defer db.Close() }
```

### Sqlite3

```go
import (   "github.com/jinzhu/gorm"   _ "github.com/jinzhu/gorm/dialects/sqlite" ) func main() {   db, err := gorm.Open("sqlite3", "/tmp/gorm.db")   defer db.Close() }
```

### SQL Server

[Get started with SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/go), it can run on your [Mac](https://sqlchoice.azurewebsites.net/en-us/sql-server/developer-get-started/go/mac/), [Linux](https://sqlchoice.azurewebsites.net/en-us/sql-server/developer-get-started/go/ubuntu/) with Docker

```go
import (   "github.com/jinzhu/gorm"   _ "github.com/jinzhu/gorm/dialects/mssql" ) func main() {   db, err := gorm.Open("mssql", "sqlserver://username:password@localhost:1433?database=dbname")   defer db.Close() }
```

## Bases de Datos no Compatibles

GORM officially supports above four databases, you could write dialects for unsupported databases, refer [GORM Dialects](/docs/dialects.html)