# Library--Management-System-in-C-
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Book {
    int id;
    char title[100];
    char author[100];
    float price;
};

struct Book books[100];
int count = 0;

// Function declarations
void addBook();
void displayBooks();
void searchBook();
void deleteBook();

int main() {
    int choice;

    while (1) {
        printf("\n====== Library Management System ======\n");
        printf("1. Add Book\n");
        printf("2. Display Books\n");
        printf("3. Search Book by ID\n");
        printf("4. Delete Book by ID\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        getchar(); // to consume newline

        switch (choice) {
            case 1:
                addBook();
                break;
            case 2:
                displayBooks();
                break;
            case 3:
                searchBook();
                break;
            case 4:
                deleteBook();
                break;
            case 5:
                printf("Exiting... Thank you!\n");
                exit(0);
            default:
                printf("Invalid choice! Try again.\n");
        }
    }
    return 0;
}

void addBook() {
    struct Book newBook;
    printf("Enter Book ID: ");
    scanf("%d", &newBook.id);
    getchar();

    printf("Enter Title: ");
    fgets(newBook.title, 100, stdin);
    newBook.title[strcspn(newBook.title, "\n")] = '\0'; // remove newline

    printf("Enter Author: ");
    fgets(newBook.author, 100, stdin);
    newBook.author[strcspn(newBook.author, "\n")] = '\0';

    printf("Enter Price: ");
    scanf("%f", &newBook.price);

    books[count++] = newBook;
    printf("✅ Book added successfully!\n");
}

void displayBooks() {
    if (count == 0) {
        printf("No books available.\n");
        return;
    }

    printf("\n------ Book List ------\n");
    for (int i = 0; i < count; i++) {
        printf("ID: %d\nTitle: %s\nAuthor: %s\nPrice: %.2f\n\n",
               books[i].id, books[i].title, books[i].author, books[i].price);
    }
}

void searchBook() {
    int id, found = 0;
    printf("Enter Book ID to search: ");
    scanf("%d", &id);

    for (int i = 0; i < count; i++) {
        if (books[i].id == id) {
            printf("\nBook Found!\n");
            printf("ID: %d\nTitle: %s\nAuthor: %s\nPrice: %.2f\n",
                   books[i].id, books[i].title, books[i].author, books[i].price);
            found = 1;
            break;
        }
    }

    if (!found)
        printf("❌ No book found with ID %d\n", id);
}

void deleteBook() {
    int id, found = 0;
    printf("Enter Book ID to delete: ");
    scanf("%d", &id);

    for (int i = 0; i < count; i++) {
        if (books[i].id == id) {
            for (int j = i; j < count - 1; j++) {
                books[j] = books[j + 1];
            }
            count--;
            printf("✅ Book deleted successfully!\n");
            found = 1;
            break;
        }
    }

    if (!found)
        printf("❌ No book found with ID %d\n", id);
}
