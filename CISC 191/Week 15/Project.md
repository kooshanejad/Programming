# Project
```java
package com.example.autompgproject;

import javax.swing.*;
import java.awt.*;
import java.io.*;
import java.sql.*;

public class Main extends JFrame {
    private JTextField userInput = new JTextField(20);
    private JSlider mpgSlider = new JSlider(JSlider.HORIZONTAL, 0, 40, 20);
    private JSlider hpSlider = new JSlider(JSlider.HORIZONTAL, 0, 150, 100);
    private JTextArea resultArea = new JTextArea(10, 70);

    public Main() {
        setTitle("Auto MPG Program");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        // Configure sliders
        mpgSlider = new JSlider(JSlider.HORIZONTAL, 9, 47, 25);  // 9–47, starting around the middle
        mpgSlider.setMajorTickSpacing(5);
        mpgSlider.setMinorTickSpacing(1);
        mpgSlider.setPaintTicks(true);
        mpgSlider.setPaintLabels(true);

        hpSlider = new JSlider(JSlider.HORIZONTAL, 45, 230, 100); // 45–230
        hpSlider.setMajorTickSpacing(25);
        hpSlider.setMinorTickSpacing(5);
        hpSlider.setPaintTicks(true);
        hpSlider.setPaintLabels(true);

        // Top panel
        JPanel topPanel = new JPanel();
        topPanel.add(new JLabel("Search Car:"));
        topPanel.add(userInput);
        JButton refreshBtn = new JButton("Refresh");
        JButton loadBtn = new JButton("Load Data");
        topPanel.add(refreshBtn);
        topPanel.add(loadBtn);

        // Slider panel
        JPanel sliderPanel = new JPanel(new GridLayout(2, 2));
        sliderPanel.add(new JLabel("Min MPG"));
        sliderPanel.add(mpgSlider);
        sliderPanel.add(new JLabel("Max Horsepower"));
        sliderPanel.add(hpSlider);

        // Result display
        resultArea.setEditable(false);
        JScrollPane scrollPane = new JScrollPane(resultArea);

        add(topPanel, BorderLayout.NORTH);
        add(sliderPanel, BorderLayout.CENTER);
        add(scrollPane, BorderLayout.SOUTH);

        // Button Actions
        refreshBtn.addActionListener(e -> fetchData());
        loadBtn.addActionListener(e -> loadData());

        pack();
        setVisible(true);
    }

    private void fetchData() {

        // Getting the filter values on the GUI
        String keyword = userInput.getText().trim();
        int mpg = mpgSlider.getValue();
        int hp = hpSlider.getValue();

        // Set up database connection info
        String url = "jdbc:mysql://localhost/auto";
        String user = "testuser";
        String password = "Pa$$word";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            PreparedStatement stmt;
            if (keyword.equalsIgnoreCase("ALL")) {
                stmt = conn.prepareStatement("SELECT * FROM auto_mpg");
            } else {
                // SQL query with placeholders for dynamic filtering
                String sql = "SELECT * FROM auto_mpg WHERE car_name LIKE ? AND mpg >= ? AND horsepower <= ?";
                stmt = conn.prepareStatement(sql);
                // setting the query parameters
                stmt.setString(1, "%" + keyword + "%"); // car name contains keyword
                stmt.setDouble(2, mpg); // minimum MPG
                stmt.setDouble(3, hp);  // maximum HP
            }

            ResultSet rs = stmt.executeQuery();

            String result = "";
            result += "MPG\tCYL\tDISP\tHP\tWEIGHT\tACCEL\tYEAR\tORIGIN\tCAR NAME\n";
            result += "------------------------------------------------------------\n";

            while (rs.next()) {
                double mpgValue = rs.getDouble("mpg");
                String mpgDisplay = (mpgValue == 0.0) ? "N/A" : String.format("%.1f", mpgValue);
                result += String.format(
                        "%s\t%d\t%.1f\t%.1f\t%.1f\t%.1f\t%d\t%d\t%s\n",
                        mpgDisplay,
                        rs.getInt("cylinders"),
                        rs.getDouble("displacement"),
                        rs.getDouble("horsepower"),
                        rs.getDouble("weight"),
                        rs.getDouble("acceleration"),
                        rs.getInt("model_year"),
                        rs.getInt("origin"),
                        rs.getString("car_name")
                );
            }

            resultArea.setText(result);
        } catch (Exception ex) {
            ex.printStackTrace();
            resultArea.setText("Error fetching data.");
        }
    }

    private void loadData() {
        String jdbcUrl = "jdbc:mysql://localhost:3306/Auto";
        String dbUser = "root";
        String dbPassword = "";

        try ( // open database and file connection
                Connection conn = DriverManager.getConnection(jdbcUrl, dbUser, dbPassword);
                // open file for reading
                BufferedReader br = new BufferedReader(new FileReader("src/main/resources/auto-mpg.data-original"))
        ) {
            String line;
            String sql = "INSERT INTO AutoData VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)";
            PreparedStatement pstmt = conn.prepareStatement(sql);

            // read each line of the dataset file
            while ((line = br.readLine()) != null) {
                // split into 9 columns
                String[] parts = line.trim().split("\\s+", 9);
                // skip incomplete rows
                if (parts.length < 9) continue;

                try {
                    setOrNull(pstmt, 1, parts[0]);    // MPG
                    setOrNullInt(pstmt, 2, parts[1]); // cylinders
                    setOrNull(pstmt, 3, parts[2]);    // displacement
                    setOrNull(pstmt, 4, parts[3]);    // horsepower
                    setOrNull(pstmt, 5, parts[4]);    // weight
                    setOrNull(pstmt, 6, parts[5]);    // acceleration
                    setOrNullInt(pstmt, 7, parts[6]); // model year
                    setOrNullInt(pstmt, 8, parts[7]); // origin
                    pstmt.setString(9, parts[8].replace("\"", ""));
                    // car name

                    pstmt.executeUpdate();
                } catch (Exception e) {
                    System.err.println("Skipping line: " + line);
                }
            }

            JOptionPane.showMessageDialog(this, "Data loaded into the database!");
        } catch (Exception e) {
            e.printStackTrace();
            JOptionPane.showMessageDialog(this, "Failed to load data.");
        }
    }

    // Helper: insert Double or null
    private void setOrNull(PreparedStatement pstmt, int index, String value) throws SQLException {
        if (value.equals("NA")) {
            pstmt.setNull(index, Types.DOUBLE);
        } else {
            pstmt.setDouble(index, Double.parseDouble(value));
        }
    }

    // Helper: insert Integer or null
    private void setOrNullInt(PreparedStatement pstmt, int index, String value) throws SQLException {
        if (value.equals("NA")) {
            pstmt.setNull(index, Types.INTEGER);
        } else {
            pstmt.setInt(index, (int) Double.parseDouble(value));
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(Main::new);
    }
}

package com.example.autompgproject;

import java.io.*;
import java.sql.*;

public class DataLoader {
    public static void main(String[] args) {
        // JDBC connection info
        String jdbcUrl = "jdbc:mysql://localhost:3306/Auto";
        String dbUser = "root";
        String dbPassword = "";

        try (
                // establishing connection to database
                Connection conn = DriverManager.getConnection(jdbcUrl, dbUser, dbPassword);

                // open dataset file for reading
                BufferedReader br = new BufferedReader(new FileReader("src/main/resources/auto-mpg.data-original"))
        ) {
            String line; // holds each line of the file
            // SQL query to insert 9 columns into the auto_mpg table
            String sql = "INSERT INTO auto_mpg VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)";

            // prepared statement for SQL query
            PreparedStatement pstmt = conn.prepareStatement(sql);

            // read the file line by line
            while ((line = br.readLine()) != null) {
                // trim the line and split it into 9 parts (the last part includes spaces)
                String[] parts = line.trim().split("\\s+", 9);
                // skip the line if it doesn't contain exactly 9 fields
                if (parts.length < 9) {
                    System.err.println("Skipping incomplete line: " + line);
                    continue;
                }

                try {
                    // handle each field individually, converting to the correct types
                    // if a field is "NA", insert a NULL into the database

                    // mpg (Double)
                    if (parts[0].equals("NA")) pstmt.setNull(1, Types.DOUBLE);
                    else pstmt.setDouble(1, Double.parseDouble(parts[0]));

                    // cylinders (Integer)
                    if (parts[1].equals("NA")) pstmt.setNull(2, Types.INTEGER);
                    else pstmt.setInt(2, (int) Double.parseDouble(parts[1]));

                    // displacement (Double)
                    if (parts[2].equals("NA")) pstmt.setNull(3, Types.DOUBLE);
                    else pstmt.setDouble(3, Double.parseDouble(parts[2]));

                    // horsepower (Double)
                    if (parts[3].equals("NA")) pstmt.setNull(4, Types.DOUBLE);
                    else pstmt.setDouble(4, Double.parseDouble(parts[3]));

                    // weight (Double)
                    if (parts[4].equals("NA")) pstmt.setNull(5, Types.DOUBLE);
                    else pstmt.setDouble(5, Double.parseDouble(parts[4]));

                    // acceleration (Double)
                    if (parts[5].equals("NA")) pstmt.setNull(6, Types.DOUBLE);
                    else pstmt.setDouble(6, Double.parseDouble(parts[5]));

                    // model year (Integer)
                    if (parts[6].equals("NA")) pstmt.setNull(7, Types.INTEGER);
                    else pstmt.setInt(7, (int) Double.parseDouble(parts[6]));

                    // origin (Integer)
                    if (parts[7].equals("NA")) pstmt.setNull(8, Types.INTEGER);
                    else pstmt.setInt(8, (int) Double.parseDouble(parts[7]));

                    // car name (String) -- removing quotes
                    pstmt.setString(9, parts[8].replace("\"", ""));

                    pstmt.executeUpdate(); // Execute the insert statement
                } catch (Exception e) {
                    // If an error occurs for a particular line, log it and skip it
                    System.err.println("Skipping line due to error: " + line);
                    e.printStackTrace();
                }

            }

            System.out.println("Data inserted successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
