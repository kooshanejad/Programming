# Derived Classes

1. Flowchart:   
![Derived Classes](https://github.com/user-attachments/assets/922aac6c-4322-45ed-8e76-5d1b5b480a9b)
2. There were not any major challenges honestly, I just had to review some of my old labs from CISC 190 in order to refresh my memory.
3. Video: https://youtube.com/shorts/lCTP5PEPs9g?feature=share
4. Code:
```java
public class Course {
    private String courseNumber;
    private String courseTitle;

    public Course(String courseNumber, String courseTitle) {
        this.courseNumber = courseNumber;
        this.courseTitle = courseTitle;
    }

    public void setCourseNumber(String courseNumber) {
        this.courseNumber = courseNumber;
    }

    public String getCourseNumber() {
        return courseNumber;
    }

    public void setCourseTitle(String courseTitle) {
        this.courseTitle = courseTitle;
    }

    public String getCourseTitle() {
        return courseTitle;
    }

    public void printInfo() {
        System.out.println("   Course Number: " + courseNumber + "\n   Course Title: " + courseTitle);
    }
}

public class OfferedCourse extends Course{
    private String instructorName;
    private String location;
    private String classTime;

    public OfferedCourse(String courseNumber, String courseTitle, String instructorName, String location, String classTime) {
        super(courseNumber, courseTitle);
        this.instructorName = instructorName;
        this.location = location;
        this.classTime = classTime;
    }

    public void setInstructorName(String instructorName) {
        this.instructorName = instructorName;
    }

    public String getInstructorName() {
        return instructorName;
    }

    public void setLocation(String location) {
        this.location = location;
    }

    public String getLocation() {
        return location;
    }

    public void setClassTime(String classTime) {
        this.classTime = classTime;
    }

    public String getClassTime() {
        return classTime;
    }

    @Override
    public void printInfo() {
        super.printInfo();
        System.out.println("   Instructor Name: " + instructorName);
        System.out.println("   Location: " + location);
        System.out.println("   Class Time: " + classTime);
    }
}

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        // Prompt user for input for the first Course
        System.out.println("Enter Course Number: ");
        String courseNum1 = input.nextLine();
        System.out.println("Enter Course Title: ");
        String courseTitle1 = input.nextLine();

        // Prompt user for input for the OfferedCourse
        System.out.println("Enter Course Number: ");
        String courseNum2 = input.nextLine();
        System.out.println("Enter Course Title: ");
        String courseTitle2 = input.nextLine();
        System.out.println("Enter Instructor Name: ");
        String instructorName = input.nextLine();
        System.out.println("Enter Location: ");
        String location = input.nextLine();
        System.out.println("Enter Class Time: ");
        String classTime = input.nextLine();

        // Create a Course object and print info
        Course course1 = new Course(courseNum1, courseTitle1);
        System.out.println("Course Information:");
        course1.printInfo();
        System.out.println();  // Space between outputs

        // Create an OfferedCourse object and print info
        OfferedCourse course2 = new OfferedCourse(courseNum2, courseTitle2, instructorName, location, classTime);
        System.out.println("Course Information:");
        course2.printInfo();

        input.close();  // Close the scanner
    }
}
```
