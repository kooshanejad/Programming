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
```
