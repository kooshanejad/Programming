# GUI

## Activity 10-11.1

1. Flowchart:   
![GUI 10-11 1](https://github.com/user-attachments/assets/c027be1d-cc71-46f5-84ee-38f63dca33b8)
2. While performing this lab, my main challenge was figuring out the syntax for the new code we learned, such as JLabel, JTextField, GridBagConstraints, etc.
3. Video: https://youtu.be/Oaox9n9_lXE
4. Code:
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

public class SalaryDemo {
    public static void main(String[] args) {
        // Creates SalaryLabelFrame and its components
        SalaryCalcFrame myFrame = new SalaryCalcFrame();

        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```

## Activity 10-11.2

1. Flowchart:   
![GUI 10-11 2](https://github.com/user-attachments/assets/44d37dc2-4846-43e8-92d4-9f3eaf7ec0af)
2. While performing this lab, my main challenge was learning the syntax for NumberFormat, JFormattedTextField, and JButton.
3. Video: https://youtu.be/5iyicxJN4LQ
4. Code:
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
import javax.swing.JOptionPane;

public class DistanceCalcFrame extends JFrame implements ActionListener {
    private JButton calcButton;              // triggers distance conversion
    private JLabel milesLabel;               // label for miles
    private JLabel kmLabel;                  // label for kilometers
    private JLabel metersLabel;              // label for meters
    private JLabel feetLabel;                // label for feet
    private JFormattedTextField milesField;  // holds miles input
    private JTextField kmField;              // displays kilometers
    private JTextField metersField;          // displays meters
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

        if (miles >= 0.0) {
            // Convert miles to km, m, and ft
            km = miles / 0.621371;
            meters = miles / 0.000621371;
            feet = miles / 0.0001893939;

            // Convert doubles to Strings and display them in their fields
            kmField.setText(Double.toString(km));
            metersField.setText(Double.toString(meters));
            feetField.setText(Double.toString(feet));
        } else {
            // Show failure dialog
            JOptionPane.showMessageDialog(this, "Enter a positive distance value!");
        }
    }
}

import javax.swing.JFrame;

public class DistanceDemo { 
    /* Creates a DistanceCalcFrame and makes it visible */
    public static void main(String[] args) {
        // Creates DistanceCalcFrame and its components
        DistanceCalcFrame myFrame = new DistanceCalcFrame();

        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```

## Activity 10-11.3

1. Flowchart:   
![GUI 10-11 3](https://github.com/user-attachments/assets/519e2a1e-9f3b-4d51-b434-8d85d94aa545)
2. While performing this lab, my main challenge was learning the syntax for JSpinner, SpinnerNumberModel, ChangeEvent, and ChangeListener.
3. Video:
4. Code:
```java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JSpinner;
import javax.swing.JTextField;
import javax.swing.SpinnerNumberModel;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;

public class DistanceCalcFrame extends JFrame implements ChangeListener {
    private JSpinner distanceSpinner;  // Triggers travel time calculation
    private JLabel milesLabel;         // Label for miles
    private JLabel kmLabel;            // Label for kilometers
    private JTextField kmField;        // Displays distance in kilometers

    /* Constructor creates GUI components and adds GUI components
    using a GridBagLayout. */
    DistanceCalcFrame() {
        int initMiles;     // Spinner initial value display
        int minMiles;  // Spinner min value
        int maxMiles;  // Spinner max value
        int stepVal;   // Spinner step

        initMiles = 0;
        minMiles = 0;
        maxMiles = 30;
        stepVal = 1;

        // Used to specify GUI component layout
        GridBagConstraints layoutConst = null;

        // Specifies the types of values displayed in spinner
        SpinnerNumberModel spinnerModel = null;

        // Set frame's title
        setTitle("Distance Conversion Calculator");

        // Create labels
        milesLabel = new JLabel("Select distance (miles):");
        kmLabel = new JLabel("Distance (km):");

        // Create a spinner model, the spinner, and set the ChangeListener
        spinnerModel = new SpinnerNumberModel(initMiles, minMiles, maxMiles, stepVal);
        distanceSpinner = new JSpinner(spinnerModel);
        distanceSpinner.addChangeListener(this);

        // Create field
        kmField = new JTextField(15);
        kmField.setEditable(false);
        kmField.setText("0");

        // Use a GridBagLayout
        setLayout(new GridBagLayout());

        // Specify component's grid location
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.anchor = GridBagConstraints.LINE_END;
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;
        add(milesLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 1;
        layoutConst.gridy = 0;
        add(distanceSpinner, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.anchor = GridBagConstraints.LINE_END;
        layoutConst.gridx = 0;
        layoutConst.gridy = 1;
        add(kmLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 1;
        layoutConst.gridy = 1;
        add(kmField, layoutConst);
    }

    @Override
    public void stateChanged(ChangeEvent event) {
        Integer miles;     // miles input

        miles = (Integer) distanceSpinner.getValue();

        // Choose output based on miles component
        switch (miles) {
            case 0:
                kmField.setText("0-15");
                break;

            case 1:
                kmField.setText("1.6093");
                break;

            case 2:
                kmField.setText("3.2187");
                break;

            case 3:
                kmField.setText("4.8280");
                break;

            case 4:
                kmField.setText("6.4374");
                break;

            case 5:
                kmField.setText("8.0467");
                break;

            case 6:
                kmField.setText("9.6561");
                break;

            case 7:
                kmField.setText("11.2654");
                break;

            case 8:
                kmField.setText("12.8748");
                break;

            case 9:
                kmField.setText("14.4841");
                break;

            case 10:
                kmField.setText("16.0934");
                break;

            case 11:
                kmField.setText("17.7028");
                break;

            case 12:
                kmField.setText("19.3121");
                break;

            case 13:
                kmField.setText("20.9215");
                break;

            case 14:
                kmField.setText("22.5308");
                break;

            case 15:
                kmField.setText("24.1402");
                break;

            default:
                kmField.setText("That's a long distance!");
        }
    }
}

import javax.swing.JFrame;

public class DistanceDemo {
    /* Creates a DistanceCalcFrame and makes it visible */
    public static void main(String[] args) {
        // Creates DistanceCalcFrame and its components
        DistanceCalcFrame myFrame = new DistanceCalcFrame();

        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```
