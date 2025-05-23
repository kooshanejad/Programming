# Project
```java
import java.sql.*;

public class Main {
    public static void main(String[] args)
        throws SQLException, ClassNotFoundException {

        // Load the JDBC driver
        Class.forName("com.mysql.cj.jdbc.Driver");
        System.out.println("Driver loaded");

        // Connect to the auto database
        Connection connection = DriverManager.getConnection(
                "jdbc:mysql://localhost/auto", "testuser", "Pa$$word");
        System.out.println("Database connected");
        }

        Statement statement = connection.createStatement();

        String createTable = """
        CREATE TABLE IF NOT EXISTS auto_mpg (
                 id INT AUTO_INCREMENT PRIMARY KEY,
                 mpg FLOAT,
                 cylinders INT,
                 displacement FLOAT,
                 horsepower FLOAT,
                 weight FLOAT,
                 acceleration FLOAT,
                 model_year INT,
                 origin INT,
                 car_name VARCHAR(100)
        )
        """;
    }
```
