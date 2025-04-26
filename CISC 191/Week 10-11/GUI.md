# GUI

Activity 1:
```java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JTextField;

public class SalaryCalcFrame extends JFrame implements ActionListener {
    private JLabel wageLabel;     // label for hourly salary
    private JLabel hourLabel;     // label for hours worked per week
    private JLabel salLabel;      // label for yearly salary
    private JTextField salField;  // displays hourly salary
    private JTextField hourField; // displays hours worked per week
    private JTextField wageField; // displays yearly salary

    /* Constructor creates GUI components and adds GUI components
    using a GridBagLayout. */
    SalaryCalcFrame() {
        // used to specify GUI component layout
        GridBagConstraints layoutConst = null;

        // set frame title
        setTitle("Salary");

        wageLabel = new JLabel("Hourly wage:");
        hourLabel = new JLabel("Hours worked per week:");
        salLabel = new JLabel("Yearly salary:");

        // set hourly salary
        wageField = new JTextField(15);
        wageField.setEditable(true);
        wageField.setText("0");
        wageField.addActionListener(this);

        // set hours worked per week
        hourField = new JTextField(15);
        hourField.setEditable(true);
        hourField.setText("0");
        hourField.addActionListener(this);

        // set annual salary
        salField = new JTextField(15);
        salField.setEditable(false);

        // Use a GridBagLayout
        setLayout(new GridBagLayout());
        layoutConst = new GridBagConstraints();

        // Specify component's grid location
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;

        // 10 pixels of padding around component
        layoutConst.insets = new Insets(10, 10, 10, 10);

        // Add component using the specified constraints
        add(wageLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.gridx = 1;
        layoutConst.gridy = 0;
        layoutConst.insets = new Insets(10, 10, 10, 10);
        add(wageField, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.gridx = 0;
        layoutConst.gridy = 1;
        layoutConst.insets = new Insets(10, 10, 10, 10);
        add(hourLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.gridx = 1;
        layoutConst.gridy = 1;
        layoutConst.insets = new Insets(10, 10, 10, 10);
        add(hourField, layoutConst);


        layoutConst = new GridBagConstraints();
        layoutConst.gridx = 0;
        layoutConst.gridy = 2;
        layoutConst.insets = new Insets(10, 10, 10, 10);
        add(salLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.gridx = 1;
        layoutConst.gridy = 2;
        layoutConst.insets = new Insets(10, 10, 10, 10);
        add(salField, layoutConst);
    }

    /* Method is automatically called when an event
     occurs (e.g, Enter key is pressed) */
    @Override
    public void actionPerformed(ActionEvent event) {
        String wageInput;      // User specified hourly wage
        String hourInput;      // User specified hours worked per week
        int hourlyWage;        // Hourly wage
        int weeklyHours;       // Hours worked per week

        // Get user's wage input and convert from String to integer
        wageInput = wageField.getText();
        hourlyWage = Integer.parseInt(wageInput);

        // Get user's hours worked input and convert from String to integer
        hourInput = hourField.getText();
        weeklyHours = Integer.parseInt(hourInput);

        // Display calculated salary
        salField.setText(Integer.toString(hourlyWage * weeklyHours * 50));
    }
}

import javax.swing.JFrame;

public static void main(String[] args) {
    // Creates SalaryLabelFrame and its components
    SalaryCalcFrame myFrame = new SalaryCalcFrame();

    myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    myFrame.pack();
    myFrame.setVisible(true);
}
```

Activity 2:
```java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.NumberFormat;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JTextField;
import javax.swing.JFormattedTextField;
import javax.swing.JButton;

public class DistanceCalcFrame extends JFrame implements ActionListener {
    private JButton calcButton;              // triggers distance conversion
    private JLabel milesLabel;               // label for miles
    private JLabel kmLabel;                  // label for kilometers
    private JLabel metersLabel;                   // label for meters
    private JLabel feetLabel;                // label for feet
    private JFormattedTextField milesField;  // holds miles input
    private JTextField kmField;              // displays kilometers
    private JTextField metersField;               // displays meters
    private JTextField feetField;            // displays feet

    /* Constructor creates GUI components and adds GUI components
    using a GridBagLayout. */
    DistanceCalcFrame() {
        // Used to specify GUI component layout
        GridBagConstraints layoutConst = null;

        // Set frame title
        setTitle("Distance Conversion Calculator");

        // Create labels
        milesLabel = new JLabel("Distance (miles):");
        kmLabel = new JLabel("Distance (kilometers):");
        metersLabel = new JLabel("Distance (meters):");
        feetLabel = new JLabel("Distance (feet): ");

        // Create button and add ActionListener
        calcButton = new JButton("Calculate");
        calcButton.addActionListener(this);

        // Create and set up an input field for numbers
        milesField = new JFormattedTextField(NumberFormat.getNumberInstance());
        milesField.setEditable(true);
        milesField.setText("0");
        milesField.setColumns(15);

        // Create kilometer field
        kmField = new JTextField(15);
        kmField.setEditable(false);

        // Create meter field
        metersField = new JTextField(15);
        metersField.setEditable(false);

        //Create feet field
        feetField = new JTextField(15);
        feetField.setEditable(false);

        // Use a GridBagLayout
        setLayout(new GridBagLayout());

        //Specify component's grid location
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;
        add(milesLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.gridx = 1;
        layoutConst.gridy = 0;
        add(milesField, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 5, 10, 10);
        layoutConst.gridx = 2;
        layoutConst.gridy = 0;
        add(calcButton, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 0, 1, 10);
        layoutConst.gridx = 1;
        layoutConst.gridy = 1;
        add(kmLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(1, 0, 10, 10);
        layoutConst.gridx = 1;
        layoutConst.gridy = 2;
        add(kmField, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 0, 1, 10);
        layoutConst.gridx = 2;
        layoutConst.gridy = 1;
        add(metersLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(1, 0, 10, 10);
        layoutConst.gridx = 2;
        layoutConst.gridy = 2;
        add(metersField, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 0, 1, 10);
        layoutConst.gridx = 3;
        layoutConst.gridy = 1;
        add(feetLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(1, 0, 10, 10);
        layoutConst.gridx = 3;
        layoutConst.gridy = 2;
        add(feetField, layoutConst);
    }
    /* Method is automatically called when an event occurs */
    @Override
    public void actionPerformed(ActionEvent event) {
        double miles;
        double km;
        double meters;
        double feet;

        // Get value from miles field
        miles = ((Number) milesField.getValue()).doubleValue();

        // Convert miles to km, m, and ft
        km = miles / 0.621371;
        meters = miles / 0.000621371;
        feet = miles / 0.0001893939;

        kmField.setText(Double.toString(km));
        metersField.setText(Double.toString(meters));
        feetField.setText(Double.toString(feet));
    }
}

import javax.swing.JFrame;

public class Main {
    public static void main(String[] args) {
        DistanceCalcFrame myFrame = new DistanceCalcFrame();

        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```
