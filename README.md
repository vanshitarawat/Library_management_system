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
    public void borrow(String input) {
			 
		        boolean found = false;
		        for (int i = 0; i < bookCount; i++) {
		            if (books[i].title.equals(input) || books[i].author.equals(input) || books[i].genre.equals(input) || books[i].isbn.equals(input)) {
		                found = true;
		                if (!books[i].isBorrowed) {
		                    books[i].isBorrowed = true;
		                    System.out.println("You have successfully borrowed: " + books[i].title);
		                } else {
		                    System.out.println("Sorry, the book is already borrowed: " + books[i].title);
		                }
		                break;
		            }
		        }
		        if (!found) {
		            System.out.println("No book found with the term: " + input);
		        }
		    }
			
		  public void returnbook(String input) {
			    boolean found = false;
			    for (int i = 0; i < bookCount; i++) {
			        if (books[i].title.equals(input) || books[i].author.equals(input) || books[i].genre.equals(input) || books[i].isbn.equals(input)) {
			            found = true;
			            if (books[i].isBorrowed) {
			                books[i].isBorrowed = false; // Mark as available
			                System.out.println("You have successfully returned: " + books[i].title);
			            } else {
			                System.out.println("The book is not currently borrowed: " + books[i].title);
			            }
			            break;
			        }
			    }
			    if (!found) {
			        System.out.println("No book found with the term: " + input);
			    }
			}

		  public void reserve(String input) {
			    boolean found = false;
			    for (int i = 0; i < bookCount; i++) {
			        if (books[i].title.equals(input) || books[i].author.equals(input) || books[i].genre.equals(input) || books[i].isbn.equals(input)) {
			            found = true;
			            if (!books[i].isreserved) {
			                books[i].isreserved = true; // Mark as reserved
			                System.out.println("You have successfully reserved: " + books[i].title);
			            } else {
			                System.out.println("The book is already reserved: " + books[i].title);
			            }
			            break;
			        }
			    }
			    if (!found) {
			        System.out.println("No book found with the term: " + input);
			    }
			}
		  public void checkOverduePenalties() {
			    boolean foundOverdue = false;

			
			    int currentDay = 24, currentMonth = 11, currentYear = 2024;

			    for (int i = 0; i < bookCount; i++) {
			        if (books[i].isBorrowed && books[i].dueDate != null) {
			            
			            String[] parts = books[i].dueDate.split("-");
			            int dueDay = Integer.parseInt(parts[0]);
			            int dueMonth = Integer.parseInt(parts[1]);
			            int dueYear = Integer.parseInt(parts[2]);

			            
			            if (currentYear > dueYear || 
			                (currentYear == dueYear && currentMonth > dueMonth) ||
			                (currentYear == dueYear && currentMonth == dueMonth && currentDay > dueDay)) {
			                
			                foundOverdue = true;

			                
			                int overdueDays = (currentYear - dueYear) * 365 + 
			                                  (currentMonth - dueMonth) * 30 + 
			                                  (currentDay - dueDay);

			                if (overdueDays < 0)
			                	overdueDays = 0; 

			                float penalty = overdueDays * 1.0f; 
			                System.out.println("Overdue Book: " + books[i].title);
			                System.out.println("Overdue Days: " + overdueDays);
			                System.out.println("Penalty: $" + penalty);
			            }
			        }
			    }

			    if (!foundOverdue) {
			        System.out.println("No overdue books found.");
			    }
public void displayAllBooks() {
			    if (bookCount == 0) {
			        System.out.println("No books available in the library.");
			        return;
			    }
			    System.out.println("\nAll Books in the Library:");
			    for (int i = 0; i < bookCount; i++) {
			        System.out.println("Book " + (i + 1) + ":");
			        books[i].display();

			        if (books[i].isBorrowed) {
			            System.out.println("Borrowed: Yes");
			        } else {
			            System.out.println("Borrowed: No");
			        }

			        if (books[i].isreserved) {
			            System.out.println("Reserved: Yes");
			        } else {
			            System.out.println("Reserved: No");
			        }

			        if (books[i].dueDate != null) {
			            System.out.println("Due Date: " + books[i].dueDate);
			        } else {
			            System.out.println("Due Date: Not Applicable");
			        }

			        System.out.println("-------------------------");
			    }
			}



		

		public static void main(String[] args) {
			Scanner sc=new Scanner(System.in);
			LibraryManagementSystem lm=new LibraryManagementSystem(100);
			while(true) {
			 System.out.println("Library Management System Menu:");
	         System.out.println("1. Add a Book");
	         System.out.println("2. Search for Book");
	         System.out.println("3. Edit a Book");
	         System.out.println("4. Remove a Book");
	         System.out.println("5. Borrow a Book");
	         System.out.println("6. Return a Book");
	         System.out.println("7. Reserve a Book");
	         System.out.println("8. Check Overdue Penalties");
	         System.out.println("9. Display");
	         System.out.println("0. Exit");
	         System.out.print("Enter your choice: ");
	         int choice = sc.nextInt();
	         sc.nextLine(); 
	switch(choice) {
	case 1:
		 System.out.println("Add title");
		 String title = sc.nextLine();

		 System.out.println("Add author");
		 String author = sc.nextLine();
		 System.out.println("Add genre");
		 String genre = sc.nextLine();
		 System.out.println("Add isbn number");
		 String isbn = sc.nextLine();
		  
		lm.add(title, author, genre, isbn);
		 System.out.println();
		break;
		
	case 2:
		  System.out.print("Enter title, author, genre, or ISBN to search: ");
	      String input = sc.nextLine();
	      lm.search(input);
	      System.out.println();
	      break;
	      
	case 3:
		System.out.print("Enter title, author, genre, or ISBN of the book you want to edit: ");
	      String edit = sc.nextLine();
	      lm.edit(edit);
	      break;
		 
	case 4:
		System.out.print("Enter title, author, genre, or ISBN of the book you want to remove: ");
		String delete=sc.nextLine();
		lm.remove(delete);
		 System.out.println();
		break;
		
	case 5:
		System.out.print("Enter title, author, genre, or ISBN of the book you want to borrow: ");
		String borrowb=sc.nextLine();
		lm.borrow(borrowb);
		 System.out.println();
			break;
			
	case 6:
		System.out.print("Enter title, author, genre, or ISBN of the book you want to return: ");
		String returnb=sc.nextLine();
		lm.returnbook(returnb);
		 System.out.println();
			break;
			
	case 7:
		System.out.print("Enter title, author, genre, or ISBN of the book you want to reserve: ");
		String reserveb=sc.nextLine();
		lm.reserve(reserveb);
		 System.out.println();
			break;
			
	case 8:
		lm.checkOverduePenalties();
		 System.out.println();
		 break;
		 
	
	case 9:
	   
lm.displayAllBooks();
break;
		
	case 0:
		 System.out.println("Exiting.....");
		 sc.close();
	return;
	
	}
	
		}
			
	}
		
	}
