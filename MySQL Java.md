## Use different methods to execute different types of queries
1. executeQuery(): for SELECT query, returns a ResultSet including all selected values
2. executeUpdat(): for non-select queries (INSERT, UPDATE, DELETE, CREATE, ALTER, etc.), returns the number of rows affected as integer
3. execute(): for any query, returns true if returns a ResultSet, returns falase if returns the integer or nothing

### Simple inseration example
```java
public class MySQLInsertion {
  // create a mysql database connection
  private static final String JDBC_DRIVER = "com.mysql.jdbc.Driver";+
  private static final String DB_NAME = "feedback";
  private static final String URL = "jdbc:mysql://localhost/" + DB_NAME + "?autoReconnect=true&useSSL=false";
  private static final String DB_USER = "root";
  private static final String DB_PWD = "pwd";
  private static Connection conn;
    
  public static void main(String[] args) {
    try {
      Class.forName(JDBC_DRIVER);
      conn = DriverManager.getConnection(URL, DB_USER, DB_PWD);

      // Create and execute insert query
      String tableName = "feedbacks";
      String rating = "5";
      String name = "Jason";
      String comment = "Awesome!";
      String query = "INSERT INTO feedbacks (rating, name, comment) VALUES(\"" + rating + "\",\"" + name + "\",\"" + comment + "\")";
      Statement stmt.executeUpdate(query);

    } catch (Exception e) {
      e.printStackTrace();
    } finally {
      if (stmt != null) {
        try {
          stmt.close();
        } catch (SQLException e) {
          e.printStackTrace();
        }
      }
    }
  }
}
```



## Errors
### WARN: Establishing SSL connection without server's identity verification is not recommended.
Add "?autoReconnect=true&useSSL=false"  
```
jdbc:mysql://localhost/table?autoReconnect=true&useSSL=false
```
