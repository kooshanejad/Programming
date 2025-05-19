# Database

1. Flowchart:   
![Database](https://github.com/user-attachments/assets/d43c8cca-7ea9-4731-a071-524d878a463a)
2. This lab had a few challenges. I had to become familiar with the commands for MySQL Shell as well as how to get the J connector to work. I also had to edit the code provided to us in the lecture to display the expected data.
3. Video: https://youtube.com/shorts/axzJrEdFtZQ?feature=share
4. Code:
```java
import java.sql.*;

public class SimpleJdbc {
    public static void main(String[] args)
            throws SQLException, ClassNotFoundException {
        // Load the JDBC driver
        Class.forName("com.mysql.cj.jdbc.Driver");
        System.out.println("Driver loaded");

        // Connect to the Miramar database
        Connection connection = DriverManager.getConnection(
                "jdbc:mysql://localhost/Miramar", "testuser", "Pa$$word");
        System.out.println("Database connected");

        // Insert the student record
        String insertSQL = "INSERT INTO Student (ssn, firstName, mi, lastName, birthDate, street, phone, zipCode, deptId) " +
                "VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)";
        PreparedStatement insertStatement = connection.prepareStatement(insertSQL);
        insertStatement.setString(1, "111222333");
        insertStatement.setString(2, "Philip");
        insertStatement.setString(3, "David Charles");
        insertStatement.setString(4, "Collins");
        insertStatement.setDate(5, Date.valueOf("1951-01-30"));
        insertStatement.setString(6, "NA");
        insertStatement.setString(7, "NA");
        insertStatement.setString(8, "NA");
        insertStatement.setInt(9, 1234);
        insertStatement.executeUpdate();

        // Update the student's zip code
        String updateSQL = "UPDATE Student SET zipCode = ? WHERE ssn = ?";
        PreparedStatement updateStatement = connection.prepareStatement(updateSQL);
        updateStatement.setString(1, "92126");
        updateStatement.setString(2, "111222333");
        updateStatement.executeUpdate();

        // Print the contents of the Student table
        Statement statement = connection.createStatement();
        ResultSet resultSet = statement.executeQuery("SELECT * FROM Student");

        while (resultSet.next()) {
            System.out.println(resultSet.getString("ssn") + "\t" +
                    resultSet.getString("firstName") + "\t" +
                    resultSet.getString("mi") + "\t" +
                    resultSet.getString("lastName") + "\t" +
                    resultSet.getString("birthDate") + "\t" +
                    resultSet.getString("street") + "\t" +
                    resultSet.getString("phone") + "\t" +
                    resultSet.getString("zipCode") + "\t" +
                    resultSet.getString("deptId"));
        }

        // Close the connection
        connection.close();
    }
}
```
