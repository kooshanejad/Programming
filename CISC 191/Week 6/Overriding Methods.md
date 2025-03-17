# Overriding Methods

1. Flowchart:   
![Overriding Methods](https://github.com/user-attachments/assets/c2a607be-5f3d-4174-b2cd-6b27acf7a422)
2. I did not really have any major challenges while performing this lab. All I had to do was review some old labs to refresh my memory.
3. Video:
4. Code:
```java
public class Book {
    private String title;
    private String author;
    private String publisher;
    private String publicationDate;

    public Book(String title, String author, String publisher, String publicationDate) {
        this.title = title;
        this.author = author;
        this.publisher = publisher;
        this.publicationDate = publicationDate;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getTitle() {
        return title;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public String getAuthor() {
        return author;
    }

    public void setPublisher(String publisher) {
        this.publisher = publisher;
    }

    public String getPublisher() {
        return publisher;
    }

    public void setPublicationDate(String publicationDate) {
        this.publicationDate = publicationDate;
    }

    public String getPublicationDate() {
        return publicationDate;
    }

    public void printInfo() {
        System.out.println("Book Information: ");
        System.out.println("   Book Title: " + title);
        System.out.println("   Author: " + author);
        System.out.println("   Publisher: " + publisher);
        System.out.println("   Publication Date: " + publicationDate);
    }
}

public class Encyclopedia extends Book{
    private String edition;
    private int pages;

    public Encyclopedia(String title, String author, String publisher, String publicationDate, String edition, int pages) {
        super(title, author, publisher, publicationDate);
        this.edition = edition;
        this.pages = pages;
    }

    public void setEdition(String edition) {
        this.edition = edition;
    }

    public String getEdition() {
        return edition;
    }

    public void setPages(int pages) {
        this.pages = pages;
    }

    public int getPages() {
        return pages;
    }

    @Override
    public void printInfo() {
        super.printInfo();
        System.out.println("   Edition: " + edition);
        System.out.println("   Number of Pages: " + pages);
    }
}

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        // Get Book information from user
        System.out.println("Enter Book Title: ");
        String title = input.nextLine();
        System.out.println("Enter Author: ");
        String author = input.nextLine();
        System.out.println("Enter Publisher: ");
        String publisher = input.nextLine();
        System.out.println("Enter Publication Date: ");
        String publicationDate = input.nextLine();

        // Get Encyclopedia-specific information from user
        System.out.println("Enter Book Title: ");
        String title2 = input.nextLine();
        System.out.println("Enter Author: ");
        String author2 = input.nextLine();
        System.out.println("Enter Publisher: ");
        String publisher2 = input.nextLine();
        System.out.println("Enter Publication Date: ");
        String publicationDate2 = input.nextLine();
        System.out.println("Enter Edition: ");
        String edition = input.nextLine();
        System.out.println("Enter Number of Pages: ");
        int pages = input.nextInt();

        // Create a Book object (first book)
        Book book = new Book(title, author, publisher, publicationDate);

        // Print book info
        book.printInfo();

        // Create an Encyclopedia object
        Encyclopedia encyclopedia = new Encyclopedia(title, author, publisher, publicationDate, edition, pages);

        // Print encyclopedia info
        encyclopedia.printInfo();

        input.close();  // Close the scanner
    }
}
```
