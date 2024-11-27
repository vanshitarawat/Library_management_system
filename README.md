# Library_management_system
import java.util.Scanner;
class Book {
    String title;
    String author;
    String genre;
    String isbn;
    boolean isBorrowed;
    boolean isreserved;
    String dueDate; 
  
    public Book(String title, String author, String genre, String isbn) {
        this.title = title;
        this.author = author;
        this.genre = genre;
        this.isbn = isbn;
        isBorrowed=false;
         isreserved=false;
         dueDate=null;
    }
    
    public void display() {
        System.out.println("Book Details: ");
        System.out.println("Title: " + this.title);
        System.out.println("Author: " + this.author);
        System.out.println("Genre: " + this.genre);
        System.out.println("ISBN: " + this.isbn);
    }
}
