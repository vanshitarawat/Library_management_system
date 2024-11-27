#Library_Management_System
package project;

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
        isBorrowed = false;
        isreserved = false;
        dueDate = null;
    }

    public void display() {
        System.out.println("Book Details: ");
        System.out.println("Title: " + this.title);
        System.out.println("Author: " + this.author);
        System.out.println("Genre: " + this.genre);
        System.out.println("ISBN: " + this.isbn);
    }
}

public class LibraryManagementSystem {
    public Book[] books;
    public int bookCount = 0;

    public LibraryManagementSystem(int size) {
        books = new Book[size];
    }

    public void add(String title, String author, String genre, String isbn) {
        if (bookCount < books.length) {
            books[bookCount++] = new Book(title, author, genre, isbn);
            System.out.println("Book added successfully: " + title);
        } else {
            System.out.println("Library is full. Cannot add more books.");
        }
    }

    public void search(String input) {
        boolean found = false;
        for (int i = 0; i < bookCount; i++) {
            if (books[i].title.equals(input) || 
                books[i].author.equals(input) || 
                books[i].genre.equals(input) || 
                books[i].isbn.equals(input)) {
                System.out.println("Book Found: " + books[i].title + " by " + books[i].author);
                found = true;
            }
        }
        if (!found) {
            System.out.println("No book found with the term");
        }
    }

    public void edit(String input) {
        boolean found = false;

        for (int i = 0; i < bookCount; i++) {
            if (books[i].title.equals(input) || 
                books[i].author.equals(input) || 
                books[i].genre.equals(input) || 
                books[i].isbn.equals(input)) {

                System.out.println("Book Found: " + books[i].title + " by " + books[i].author);
                found = true;

                Scanner sc = new Scanner(System.in);

                System.out.println("Enter new title (leave blank to keep current): ");
                String newTitle = sc.nextLine();
                if (!newTitle.isEmpty()) {
                    books[i].title = newTitle;
                }

                System.out.println("Enter new author (leave blank to keep current): ");
                String newAuthor = sc.nextLine();
                if (!newAuthor.isEmpty()) {
                    books[i].author = newAuthor;
                }

                System.out.println("Enter new genre (leave blank to keep current): ");
                String newGenre = sc.nextLine();
                if (!newGenre.isEmpty()) {
                    books[i].genre = newGenre;
                }

                System.out.println("Enter new ISBN (leave blank to keep current): ");
                String newIsbn = sc.nextLine();
                if (!newIsbn.isEmpty()) {
                    books[i].isbn = newIsbn;
                }
            }
        }
        if (!found) {
            System.out.println("No book found with the term: " + input);
        }
    }

    public void remove(String input) {
        boolean found = false;
        for (int i = 0; i < bookCount; i++) {
            if (books[i].title.equals(input) || books[i].author.equals(input) || books[i].genre.equals(input) || books[i].isbn.equals(input)) {
                found = true;
                System.out.println("Removing book: " + books[i].title + " by " + books[i].author);
                for (int j = i; j < bookCount - 1; j++) {
                    books[j] = books[j + 1];
                }
                bookCount--;
                books[bookCount] = null;

                System.out.println("Book removed successfully.");
                break;
            }
        }
        if (!found) {
            System.out.println("No book found with the term: " + input);
        }
    }
