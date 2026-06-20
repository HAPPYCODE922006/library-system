import json
import tkinter as tk

#function
def load_books():
    try:
        with open("books.json", "r") as file:
            return json.load(file)
    except FileNotFoundError:
        return []
books = load_books()  # Load books at the start of the program
print("loaded books:", books)


def save_books(books):
    with open("books.json", "w") as file:
        json.dump(books, file)
    print("books saved:", books)

# Class
class Library:
    def __init__(self):
        self.books = load_books()
          # Load books when the library is initialized
#book added
    def add_book(self):
        book_name = book_name_entry.get()
        author = author_entry.get()
        quantity =int(quantity_entry.get())
        #check if the book already exists
        for book in self.books:
            if book["book_name"].lower() == book_name.lower():
                book["quantity"] += quantity  # Update quantity if book already exists
                save_books(self.books)  # Save after updating the quantity
                print("book already exists")
                return
        book = {
            "book_name": book_name,
            "author": author,
            "quantity": quantity,
}
    
        print("book added successfully")
        self.books.append(book)
        save_books(self.books)  # Save after adding a book
        print(books)
    


#book viewed
    def view_books(self):
      print("book viewed")
      print("books variable:", self.books)  # Debugging statement to check the contents of books
      for book in self.books:
        
        print(book)

#book searched
    def search_book(self):
      print("search book you waant" )
      enter_book_name = input("Enter book_name to search: ")
      found = False
      for book in self.books:
        if book["book_name"].lower()==enter_book_name.lower():
         print("book found")
         print(book)
         found = True
         break
      if not found:
            print("book not found")
        
      
#book removed
    def remove_book(self):
       enter_book_name = input("Enter book_name to remove: ")
       removed = False 
       for book in self.books:
           if book["book_name"].lower() == enter_book_name.lower():
            self.books.remove(book)
            save_books(self.book)
            print("book removed successfully")
            removed = True
            break
       if not removed:
                print("book not removed")
     


#book issued    
    def issue_book(self):
       enter_book_name = input("Enter book_name to issue: ")
       issued = False 
       for book in self.books:
          if book["book_name"].lower() == enter_book_name.lower():
            if book["quantity"] > 0:
                book["quantity"] -= 1
                save_books(self.books)  # Save after issuing a book
                print("book issued successfully")
                issued = True
            else:
                print("book not available")
            return
       
    print("book not issued")


#book returned
    def return_book(self):
       enter_book_name = input("Enter book_name to return: ")  
       returned = False
       for book in self.books:
            if book["book_name"].lower() == enter_book_name.lower():
                book["quantity"] += 1
                save_books(self.books)  # Save after returning a book
                returned = True
                break
       if not returned:
        print("book not found")
       else:   
         print("book returned")
#create object
library = Library()

#tkinter gui
window = tk.Tk()
window.title("Library Management System")
window.geometry("700x600")

title= tk.Label(window, text="Library Management System", font=("Arial", 23, "bold" ), fg="blue"    )

title.pack()

tk.Label(window, text="").pack()  # Add some space between the title and the buttons
library = Library()     
view_books_button = tk.Button(window, text="View Books", font=("Arial", 14),bg="lightgray",fg="navy", width=20, command=library.view_books)
view_books_button.pack(pady=10)
search_book_button = tk.Button(window, text="Search Book", font=("Arial", 14),bg="lightgray",fg="navy", width=20, command=library.search_book)
search_book_button.pack(pady=10)
remove_book_button = tk.Button(window, text="Remove Book", font=("Arial", 14),bg="lightgray",fg="navy", width=20, command=library.remove_book)
remove_book_button.pack(pady=10)
issue_book_button = tk.Button(window, text="Issue Book", font=("Arial", 14),bg="lightgray",fg="navy", width=20, command= library.issue_book)
issue_book_button.pack(pady=10)
return_book_button = tk.Button(window, text="Return Book", font=("Arial", 14),bg="lightgray",fg="navy", width=20, command= library.return_book)
return_book_button.pack(pady=10)

book_name_entry = tk.Entry(window)
tk.Label(window,fg="navy",text="Book Name").pack()
book_name_entry.pack()
author_entry = tk.Entry(window)
tk.Label(window, text="Author").pack()
author_entry.pack()

quantity_entry = tk.Entry(window)
tk.Label(window, text="Quantity").pack()
quantity_entry.pack()
search_entry=tk.Entry(window)


window.mainloop()



while True:
    print("1. Add Book")
    print("2. View Books")
    print("3. Search Book")
    print("4. Remove Book")
    print("5. Issue Book")
    print("6. Return Book")         
    a=input("enter your choice;  ")
    if a == "1":
        library.add_book()
    elif a == "2":
        library.view_books()
    elif a == "3":
        library.search_book()
    elif a == "4":
         library.remove_book()
    elif a == "5":
         library.issue_book()
    elif a == "6":
        library.return_book()
  
    elif a == "7":
        break

