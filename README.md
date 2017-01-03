# DataSpread Software Release 

DataSpread is a _spreadsheet-database hybrid system_, with a spreadsheet frontend, and a database backend. Thus, DataSpread inherits the flexibility and ease-of-use of spreadsheets, as well as the scalability and power of databases. DataSpread is a multi-year project, supported by the National Science Foundation via award number 1633755.

### Version
The current version is 0.1.

### Features
DataSpread is built using [PostgreSQL][postgressite] and [ZKSpreadsheet][zksite], an open-source web-based spreadsheet tool.

DataSpread's version 0.1 enables users to scale to **billions of cells and return results for common spreadsheet operations within seconds**. It does so via on-demand loading of spreadsheet data.


Like traditional spreadsheet software, DataSpread supports standard spreadsheet book and sheet operations like Load, Rename, Delete, and Import (via XLS and XLSX, and CSV). Any updates to the spreadsheets are automatically saved.

Like traditional spreadsheet software, DataSpread supports the use of 225+ spreadsheet functions, along with formatting and styling operations. It also supports row and column operations like insert, delete, cut, copy, and paste; during insertion and deletion, formulae are updated as is the case in traditional spreadsheet software. 

It supports all these operations while scaling to *arbitrarily large* spreadsheets.

In future releases, DataSpread will support SQL on the spreadsheet frontend, along with other relational algebra-based interactions. It will also support joint formula evaluation and optimization. 

### Key Design Innovations

* DataSpread employs a _flexible hybrid data model_ to represent spreadsheet data within a database. 
* DataSpread uses _positional indexing techniques_ to both locate data by position, and keep it up-to-date as the data is updated. 
* DataSpread also employs a _LRU caching mechanism_ to retrieve and keep in memory data from the database on demand. 
* DataSpread also employs _speculative fetching_ to fetch additional data beyond the user's current spreadsheet window. 



## Setup Instructions:

You can directly use DataSpread via our cloud-hosted [site][siteinfo].

To host DataSpread locally you can either use one of the pre-build war files, available [here][warlink], or build the war file yourself from the source.

### Required Software

* [Apache Ant][ant] >= 1.6
* [Java Platform (JDK)][java] >= 8
* [PostgreSQL][posrgres] >= 9.5
* [PostgreSQL JDBC driver][jdbc] 9.4.1208
* [Apache Tomcat][tomcat] >= 8.5.4


### Building Instructions (To generate a war file)

1. Clone the DataSpread repository. Alternatively, you can download the source as a zip. 

2. Use Ant to build the `war` file.  After the build completes the war is available at `out/artifacts/DataSpread_war`. 

	```
	ant
	```

### Deploying DataSpread locally. 


1. Install PostgresSQL.  Create a database and an user who has access to the database.  Note the database name, username and password.  

2. Install Apache Tomcat. 

3. Update web.xml in Tomcat by adding the following text:

	```
	<listener>
	    <listener-class>org.zkoss.zss.model.impl.DBHandler</listener-class>
	</listener>
	```

4. Update context.xml in Tomcat by adding the following text:
	```
	<Resource name="jdbc/ibd" auth="Container"
	          type="javax.sql.DataSource" driverClassName="org.postgresql.Driver"
	          url="jdbc:postgresql://127.0.0.1:5432/<database_name>"
	          username="<username>" password="<password>"
                  maxTotal="20" maxIdle="10" maxWaitMillis="-1" defaultAutoCommit="false" accessToUnderlyingConnectionAllowed="true"/>
	```

	Replace `<database_name>`, `<username>` and `<password>` with your PostgreSQL's database name, user name and password respectively.

5. Copy `postgresql-9.4.1208` to Tomcat lib. It is crucial to have the exact version of this file. 
 
6. Deploy the war file within Tomcat. 

7. Now you are ready to run the program. Visit the url (listed in `context.xml` above) where you have deployed the application. 


License
----
MIT

[jdbc]: https://jdbc.postgresql.org/download/postgresql-9.4.1208.jar
[ant]: https://ant.apache.org/bindownload.cgi
[tomcat]: http://tomcat.apache.org/download-80.cgi
[java]: http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html
[posrgres]:[https://www.postgresql.org/download/]
[siteinfo]: http://kite.cs.illinois.edu:8080
[zksite]: https://www.zkoss.org/product/zkspreadsheet
[postgressite]: https://www.postgresql.org/
[warlink]: http://google.com
