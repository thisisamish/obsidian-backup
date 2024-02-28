- JDBC API: A set of interfaces and classes from Java API and it is vendor-neutral.
- Classes:
	- DriverManager class is bootstrap class to start with database connectivity.
	- SQLException (child class of Exception class) to handle database related errors.
- Interfaces:
	- Driver
	- Connection
	- Statement
	- PreparedStatement
	- CallableStatement
	- ResultSet
- Database Driver: is the implementation of JDBC API. It is supplied by database vendor.
- Steps for database connectivity:
	1. Download the database driver from the vendor.
	2. Add database driver (.jar) in the project class path.
	3. Load Database Driver class (we can skip this as this was supposed to be done in earlier versions of Java).
	4. Connect to the database.
- The code is given below:
	```java
	String connectionUrl =
                "jdbc:sqlserver://192.168.134.164:1433;"
                        + "database=db83;"
                        + "user=user83;"
                        + "password=db83;"
                        + "encrypt=false;"
                        + "trustServerCertificate=false;"
                        + "loginTimeout=30;";

		ResultSet resultSet = null;

        try (Connection connection = DriverManager.getConnection(connectionUrl);
            Statement statement = connection.createStatement();) {

            String selectSql = "SELECT * from dbo.Books";
            resultSet = statement.executeQuery(selectSql);

            while (resultSet.next()) {
                System.out.println(resultSet.getString(1) + " " +
                		resultSet.getString(2) + " " + resultSet.getString(3) + " " + 
                		resultSet.getString(4) + " " + resultSet.getString(5) + " " + 
                		resultSet.getString(6) + " " + resultSet.getString(7) + " " +
                		resultSet.getString(8));
            }
        }
        catch (SQLException e) {
            e.printStackTrace();
        }
```
- DAO - Data Access Object Design Pattern