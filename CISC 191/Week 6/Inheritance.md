# Inheritance

1. Flowchart:   
![Inheritance](https://github.com/user-attachments/assets/dcc2c8a3-7904-43c1-b621-826b07403e05)
2. This lab was pretty simple honestly, I did not really have any major challenges.
3. Video:
4. Code:

```java

public class Person {
    private int ageYears;
    private String lastName;

    public void setName(String userName) {
        lastName  = userName;
    }

    public void setAge(int numYears) {
        ageYears = numYears;
    }

    // Other parts omitted

    public void printAll() {
        System.out.print("Name: " + lastName);
        System.out.print(", Age: "  + ageYears);
    }
}

public class Student extends Person {
    private int idNum;

    public void setID(int studentId) {
        idNum = studentId;
    }

    public int getID() {
        return idNum;
    }
}

public class StudentDerivationFromPerson {
    public static void main(String[] args) {
        Student courseStudent = new Student();

        courseStudent.setName("Smith");
        courseStudent.setAge(20);
        courseStudent.setID(9999);

        courseStudent.printAll();
        System.out.println(", ID: " + courseStudent.getID());

    }
}

```
