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
