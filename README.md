- 👋 Hi, I’m @Helpingmax
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Helpingmax/Helpingmax is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Book {
    private int id;
    private String title;
    private String author;
    private boolean isAvailable;

    public Book(int id, String title, String author) {
        this.id = id;
        this.title = title;
        this.author = author;
        this.isAvailable = true;
    }

    // Getters and toString method
    public boolean isAvailable() {
        return isAvailable;
    }

    public void setAvailable(boolean available) {
        isAvailable = available;
    }

    @Override
    public String toString() {
        return "Book{" + "id=" + id + ", title='" + title + '\'' + ", author='" + author + '\'' + '}';
    }
}

class User {
    private int userId;
    private String name;
    private List<Book> borrowedBooks;

    public User(int userId, String name) {
        this.userId = userId;
        this.name = name;
        this.borrowedBooks = new ArrayList<>();
    }

    // Borrow and return methods
    public void borrowBook(Book book) {
        if (book.isAvailable()) {
            borrowedBooks.add(book);
            book.setAvailable(false);
            System.out.println(name + " borrowed " + book);
        } else {
            System.out.println("Book is not available.");
        }
    }

    public void returnBook(Book book) {
        if (borrowedBooks.remove(book)) {
            book.setAvailable(true);
            System.out.println(name + " returned " + book);
        } else {
            System.out.println("This book was not borrowed.");
        }
    }
}

class Library {
    private List<Book> books;
    private List<User> users;

    public Library() {
        books = new ArrayList<>();
        users = new ArrayList<>();
    }

    public void addBook(Book book) {
        books.add(book);
        System.out.println("Added: " + book);
    }

    public void registerUser(User user) {
        users.add(user);
        System.out.println("Registered: " + user.name);
    }

    public void borrowBook(User user, Book book) {
        if (books.contains(book)) {
            user.borrowBook(book);
        } else {
            System.out.println("Book not found in the library.");
        }
    }

    public void returnBook(User user, Book book) {
        user.returnBook(book);
    }
}

public class LibraryManagementSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Library library = new Library();

        // Sample data
        library.addBook(new Book(1, "1984", "George Orwell"));
        library.addBook(new Book(2, "To Kill a Mockingbird", "Harper Lee"));
        library.registerUser(new User(1, "Alice"));

        // Menu for interaction
        while (true) {
            System.out.println("1. Borrow Book\n2. Return Book\n3. Exit");
            int choice = scanner.nextInt();
            switch (choice) {
                case 1:
                    System.out.println("Enter user ID and book ID to borrow:");
                    int userId = scanner.nextInt();
                    int bookId = scanner.nextInt();
                    // Assuming we only have one user and searching by ID
                    User user = library.users.get(0);  // Simplified for demo
                    Book book = library.books.get(bookId - 1); // Assuming book IDs are sequential
                    library.borrowBook(user, book);
                    break;
                case 2:
                    System.out.println("Enter user ID and book ID to return:");
                    userId = scanner.nextInt();
                    bookId = scanner.nextInt();
                    user = library.users.get(0); // Simplified
                    book = library.books.get(bookId - 1);
                    library.returnBook(user, book);
                    break;
                case 3:
                    System.exit(0);
            }
        }
    }
}
