# Input and Output

1. Flowchart:   
![Input and Output](https://github.com/user-attachments/assets/badcff68-1dad-452d-a6d3-d3f59260640e)
2. The lab was not very challenging apart from reviewing topics I learned in my beginner Java class. I reviewed some of my old labs to help with this.
3. https://youtube.com/shorts/BulWdGYO1Ds?feature=share   
4. Code:
```java
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        // Prompt user for file name
        System.out.print("Enter the name of the text file: ");
        String fileName = input.nextLine();

        File file = new File(fileName);

        try (Scanner fileScanner = new Scanner(file)) {
            while (fileScanner.hasNextLine()) {
                String photoFileName = fileScanner.nextLine();

                // Replace "_photo.jpg" with "_info.txt"
                String infoFileName = photoFileName.replace("_photo.jpg", "_info.txt");

                System.out.println(infoFileName);
            }
        } catch (FileNotFoundException e) {
            System.out.println("File not found.");
        }

        input.close();
    }
}
```
