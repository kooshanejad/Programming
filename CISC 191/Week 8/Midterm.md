# Midterm

Version 1.0:   
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        // get painkiller details
        System.out.println("Enter item name: ");
        String itemName = input.nextLine();
        System.out.println("Enter drug company name: ");
        String companyName = input.nextLine();
        System.out.println("Enter expiry date: ");
        String expiryDate = input.nextLine();
        System.out.println("Enter age group: ");
        String ageGroup = input.nextLine();
        Painkillers painkiller = new Painkillers(itemName, companyName, expiryDate, ageGroup);

        // get bandage details
        System.out.println("Enter item name: ");
        itemName = input.nextLine();
        System.out.println("Enter company name: ");
        companyName = input.nextLine();
        System.out.println("Enter expiry date: ");
        expiryDate = input.nextLine();
        System.out.println("Enter age group: ");
        ageGroup = input.nextLine();
        System.out.println("Is the item waterproof? (yes/no) ");
        String waterProof = input.nextLine();
        Bandages bandage = new Bandages(itemName, companyName, expiryDate, ageGroup, waterProof);

        // get equipment details
        System.out.println("Enter item name: ");
        itemName = input.nextLine();
        System.out.println("Enter company name: ");
        companyName = input.nextLine();
        System.out.println("Enter item weight (lbs): ");
        String weight = input.nextLine();
        Equipment equipment = new Equipment(itemName, companyName, weight);

        // display entered info
        System.out.println("\nInventory details:");
        painkiller.displayInfo();
        bandage.displayInfo();
        equipment.displayInfo();

        input.close();
    }
}

public class Aisle {
    protected String itemName;
    protected String companyName;

    public Aisle(String itemName, String companyName) {
        this.itemName = itemName;
        this.companyName = companyName;
    }

    public void displayInfo() {
        System.out.println("Item name: " + itemName);
        System.out.println("Company: " + companyName);
    }
}

public class Painkillers extends Aisle {
    private String expiryDate;
    private String ageGroup;

    public Painkillers(String itemName, String companyName, String expiryDate, String ageGroup) {
        super(itemName, companyName);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
    }

    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Expiry date: " + expiryDate);
        System.out.println("Age group: " + ageGroup);
    }
}

public class Bandages extends Aisle {
    private String expiryDate;
    private String ageGroup;
    private String waterProof;

    public Bandages(String itemName, String companyName, String expiryDate, String ageGroup, String waterProof) {
        super(itemName, companyName);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
        this.waterProof = waterProof;
    }

    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Expiry date: " + expiryDate);
        System.out.println("Age group: " + ageGroup);
        System.out.println("Waterproof: " + waterProof);
    }
}

public class Equipment extends Aisle {
    private String weight;

    public Equipment(String itemName, String companyName, String weight) {
        super(itemName, companyName);
        this.weight = weight;
    }

    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Item weight (lbs): " + weight);
    }
}
```

Version 2.0:   
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        try {
            // Get painkiller details
            System.out.println("Enter item name: ");
            String itemName = input.nextLine();
            System.out.println("Enter drug company name: ");
            String companyName = input.nextLine();
            System.out.println("Enter expiry date: ");
            String expiryDate = input.nextLine();
            System.out.println("Enter age group: ");
            String ageGroup = input.nextLine();
            Painkillers painkiller = new Painkillers(itemName, companyName, expiryDate, ageGroup);

            // Get bandage details
            System.out.println("Enter item name: ");
            itemName = input.nextLine();
            System.out.println("Enter company name: ");
            companyName = input.nextLine();
            System.out.println("Enter expiry date: ");
            expiryDate = input.nextLine();
            System.out.println("Enter age group: ");
            ageGroup = input.nextLine();
            System.out.println("Is the item waterproof? (yes/no) ");
            String waterProof = input.nextLine();

            // Validate waterproof input
            if (!waterProof.equalsIgnoreCase("yes") && !waterProof.equalsIgnoreCase("no")) {
                throw new IllegalArgumentException("Invalid input for waterproof. Please enter 'yes' or 'no'.");
            }

            Bandages bandage = new Bandages(itemName, companyName, expiryDate, ageGroup, waterProof);

            // Get equipment details
            System.out.println("Enter item name: ");
            itemName = input.nextLine();
            System.out.println("Enter company name: ");
            companyName = input.nextLine();
            System.out.println("Enter item weight (lbs): ");
            String weight = input.nextLine();

            // Validate weight input (empty or spaces)
            if (weight.trim().equals("")) {
                throw new IllegalArgumentException("Weight cannot be empty.");
            }

            // Create the Equipment object
            Equipment equipment = new Equipment(itemName, companyName, weight);

            // Display entered info
            System.out.println("\nInventory details:");
            painkiller.displayInfo();
            bandage.displayInfo();
            equipment.displayInfo();

        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        } finally {
            input.close();
        }
    }
}

public class Aisle {
    protected String itemName;
    protected String companyName;

    public Aisle(String itemName, String companyName) {
        this.itemName = itemName;
        this.companyName = companyName;
    }

    public void displayInfo() {
        System.out.println("Item name: " + itemName);
        System.out.println("Company: " + companyName);
    }
}

public class Painkillers extends Aisle {
    private String expiryDate;
    private String ageGroup;

    public Painkillers(String itemName, String companyName, String expiryDate, String ageGroup) {
        super(itemName, companyName);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
    }

    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Expiry date: " + expiryDate);
        System.out.println("Age group: " + ageGroup);
    }
}

public class Bandages extends Aisle {
    private String expiryDate;
    private String ageGroup;
    private String waterProof;

    public Bandages(String itemName, String companyName, String expiryDate, String ageGroup, String waterProof) {
        super(itemName, companyName);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
        this.waterProof = waterProof;
    }

    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Expiry date: " + expiryDate);
        System.out.println("Age group: " + ageGroup);
        System.out.println("Waterproof: " + waterProof);
    }
}

public class Equipment extends Aisle {
    private String weight;

    public Equipment(String itemName, String companyName, String weight) {
        super(itemName, companyName);
        this.weight = weight;
    }

    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Item weight (lbs): " + weight);
    }
}
```

Version 3.0:   
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

            // Get painkiller details
            System.out.println("Enter item name: ");
            String itemName = input.nextLine();
            System.out.println("Enter drug company name: ");
            String companyName = input.nextLine();
            System.out.println("Enter expiry date: ");
            String expiryDate = input.nextLine();
            System.out.println("Enter age group: ");
            String ageGroup = input.nextLine();
            Painkillers painkiller = new Painkillers(itemName, companyName, expiryDate, ageGroup);

            // Get bandage details
            System.out.println("Enter item name: ");
            itemName = input.nextLine();
            System.out.println("Enter company name: ");
            companyName = input.nextLine();
            System.out.println("Enter expiry date: ");
            expiryDate = input.nextLine();
            System.out.println("Enter age group: ");
            ageGroup = input.nextLine();
            System.out.println("Is the item waterproof? (yes/no) ");
            String waterProof = input.nextLine();
            Bandages bandage = new Bandages(itemName, companyName, expiryDate, ageGroup, waterProof);

            // Get equipment details
            System.out.println("Enter item name: ");
            itemName = input.nextLine();
            System.out.println("Enter company name: ");
            companyName = input.nextLine();

            String weight = "";
            boolean validWeight = false;

            while (!validWeight) {
                System.out.println("Enter item weight (lbs): ");
                weight = input.nextLine();
                try {
                    if (weight.trim().length() == 0) {
                        throw new InvalidInputException("Weight cannot be empty!");
                    }
                    validWeight = true;
                } catch (InvalidInputException e) {
                    System.out.println("Error: " + e.getMessage());
                }
            }

            // Create the Equipment object
            Equipment equipment = new Equipment(itemName, companyName, weight);

            // Display entered info
            System.out.println("\nInventory details:");
            painkiller.displayInfo();
            bandage.displayInfo();
            equipment.displayInfo();

            input.close();
    }
}

public class InvalidInputException extends Exception {
    public InvalidInputException(String message) {
        super(message);  // Call the constructor of Exception class
    }
}

public class Aisle {
    protected String itemName;
    protected String companyName;

    public Aisle(String itemName, String companyName) {
        this.itemName = itemName;
        this.companyName = companyName;
    }

    public void displayInfo() {
        System.out.println("Item name: " + itemName);
        System.out.println("Company: " + companyName);
    }
}

public class Painkillers extends Aisle {
    private String expiryDate;
    private String ageGroup;

    public Painkillers(String itemName, String companyName, String expiryDate, String ageGroup) {
        super(itemName, companyName);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
    }

    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Expiry date: " + expiryDate);
        System.out.println("Age group: " + ageGroup);
    }
}

public class Bandages extends Aisle {
    private String expiryDate;
    private String ageGroup;
    private String waterProof;

    public Bandages(String itemName, String companyName, String expiryDate, String ageGroup, String waterProof) {
        super(itemName, companyName);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
        this.waterProof = waterProof;
    }

    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Expiry date: " + expiryDate);
        System.out.println("Age group: " + ageGroup);
        System.out.println("Waterproof: " + waterProof);
    }
}

public class Equipment extends Aisle {
    private String weight;

    public Equipment(String itemName, String companyName, String weight) {
        super(itemName, companyName);
        this.weight = weight;
    }

    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Item weight (lbs): " + weight);
    }
}
```
