# Salary Calculation

1. Flowchart:  
![Salary Calculation](https://github.com/user-attachments/assets/31d98400-7fa7-45f9-9003-32fd0493e980)

2. My main challenge was remembering some of the basics we learned in Java. Besides that, it wasn't really hard.
3. Video: https://youtu.be/K28EQj3zGoA
4. Code:
```java
import java.util.Scanner;

public class IncomeTaxMain {
    public static void main(String[] args) {
        final String PROMPT_SALARY = "\nEnter annual salary (-1 to exit)";
        Scanner input = new Scanner(System.in);
        int annualSalary;
        double taxRate;
        int taxToPay;


        // Modified salary ranges and tax rates
        int[] salaryRange = {0, 30000, 60000, Integer.MAX_VALUE};
        double[] taxRates = {0.0, 0.25, 0.35, 0.45};


        // Use the overloaded constructor to initialize salary and tax rate tables
        TaxTableTools table = new TaxTableTools(salaryRange, taxRates);


        // Get the first annual salary to process
        annualSalary = table.getInteger(input, PROMPT_SALARY);


        while (annualSalary >= 0) {
            taxRate = table.getValue(annualSalary);
            taxToPay = (int) (annualSalary * taxRate); // Truncate tax to an integer amount
            System.out.println("Annual Salary: " + annualSalary +
                    "\tTax rate: " + taxRate +
                    "\tTax to pay: " + taxToPay);


            // Get the next annual salary
            annualSalary = table.getInteger(input, PROMPT_SALARY);
        }
    }
}

import java.util.Scanner;


public class TaxTableTools {


    private int[] search = {0, 20000, 50000, 100000, Integer.MAX_VALUE};
    private double[] value = {0.0, 0.10, 0.20, 0.30, 0.40};
    private int nEntries;

    public TaxTableTools() {
        nEntries = search.length;
    }


    // Overloaded constructor
    public TaxTableTools(int[] newSearch, double[] newValue) {
        this.search = newSearch;
        this.value = newValue;
        this.nEntries = newSearch.length;
    }


    // Setter method
    public void setTaxTable(int[] newSearch, double[] newValue) {
        this.search = newSearch;
        this.value = newValue;
        this.nEntries = newSearch.length;
    }


    public int getInteger(Scanner input, String prompt) {
        int inputValue = 0;


        System.out.println(prompt + ": ");
        inputValue = input.nextInt();


        return inputValue;
    }


    public double getValue(int searchArgument) {
        double result = 0.0;
        boolean keepLooking = true;
        int i = 0;


        while ((i < nEntries) && keepLooking) {
            if (searchArgument <= search[i]) {
                result = value[i];
                keepLooking = false;
            } else {
                ++i;
            }
        }


        return result;
    }
}
```
