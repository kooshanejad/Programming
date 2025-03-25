# Mock Midterm

```java
public class Aisle {
    protected String location;

    public Aisle(String location) {
        this.location = location;
    }

    public void displayInfo() {
        System.out.println("Location: " + location);
    }

}

public class Paints extends Aisle {
    private String paintCompany;
    private String type;

    public Paints(String paintCompany, String type, String location) {
        super(location);
        this.paintCompany = paintCompany;
        this.type = type;
    }

    @Override
    public void displayInfo() {
        System.out.println("Paint Company: " + paintCompany);
        System.out.println("Type: " + type);
        super.displayInfo();
    }

}

public class BrushesAndRollers extends Aisle {
    private String brushType;

    public BrushesAndRollers(String brushType, String location) {
        super(location);
        this.brushType = brushType;
    }

    @Override
    public void displayInfo() {
        System.out.println("Brush Type: " + brushType);
        super.displayInfo();
    }
}

public class Accessories extends Aisle {
    private String accessory;

    public Accessories(String accessory, String location) {
        super(location);
        this.accessory = accessory;
    }

    @Override
    public void displayInfo() {
        System.out.println("Accessory Type: " + accessory);
        super.displayInfo();
    }

}

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        // Get Paint details
        System.out.print("Enter paint company name: ");
        String paintCompany = input.nextLine();
        System.out.print("Enter paint type (Gloss, Semi-gloss, Flat): ");
        String paintType = input.nextLine();
        System.out.print("Enter paint location: ");
        String paintLocation = input.nextLine();
        Paints paint = new Paints(paintCompany, paintType, paintLocation);

        // Get Brush/Roller details
        System.out.print("Enter brush/roller type: ");
        String brushType = input.nextLine();
        System.out.print("Enter brush/roller location: ");
        String brushLocation = input.nextLine();
        BrushesAndRollers brushes = new BrushesAndRollers(brushType, brushLocation);

        // Get Accessory details
        System.out.print("Enter accessory name: ");
        String accessoryName = input.nextLine();
        System.out.print("Enter accessory location: ");
        String accessoryLocation = input.nextLine();
        Accessories accessory = new Accessories(accessoryName, accessoryLocation);

        // Display entered data
        System.out.println("\nInventory Details:");
        paint.displayInfo();
        brushes.displayInfo();
        accessory.displayInfo();

        input.close();
    }
}
```
