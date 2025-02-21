# Memory Management

1. Flowchart:   
![Memory Management](https://github.com/user-attachments/assets/472706da-17f1-439d-9a3a-2e51756cc1ff)
2. What were your challenges in performing the lab (from design to the implementation phases)? (2 mark).
3. Create a video explaining how the code works. The video should show your face on one side of the screen preferably the top or bottom right of the screen. (1 mark)
4. Code:   
```java
class Person {
    String name;
    int age;

    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Method to display details
    public void display() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

public class StackHeapExample {
    public static void main(String[] args) {
        Person p1 = new Person("Alice", 25);
        Person p2 = new Person("Bob", 30);

        p1.display();
        p2.display();

        p1 = null; // Marking object for garbage collection
    }
}
```
![StackHeap](https://github.com/user-attachments/assets/1e700ef2-5244-4fd1-8fe4-580583fcc3e8)
