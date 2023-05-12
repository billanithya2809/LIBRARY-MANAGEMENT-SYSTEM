# LIBRARY-MANAGEMENT-SYSTEM
# Import necessary modules
import getpass

# Define username and password
username = "admin"
password = "password123"

# Define list of books in the library and their prices
books = {"The Great Gatsby": 10.99, "To Kill a Mockingbird": 8.99, "1984": 12.99, "Pride and Prejudice": 7.99}

# Create login function
def login():
    # Get user input
    user = input("Username: ")
    passw = getpass.getpass("Password: ")
   
    # Check if username and password are correct
    if user == username and passw == password:
        print("Login successful!")
        # Call function to display user dashboard
        display_dashboard()
    else:
        print("Incorrect username or password. Please try again.")
        # Call function again to allow user to retry login
        login()

# Create function to display user dashboard
def display_dashboard():
    print("Welcome to the Library Management System!")
    print("1. View books")
    print("2. Choose books")
    print("3. Pay bill")
    print("4. Quit")
   
    # Get user input
    choice = input("Enter your choice: ")
   
    # Process user input
    if choice == "1":
        display_books()
    elif choice == "2":
        choose_books()
    elif choice == "3":
        pay_bill()
    elif choice == "4":
        print("Goodbye!")
    else:
        print("Invalid choice. Please try again.")
        display_dashboard()

# Create function to display all books in the library
def display_books():
    print("Books in the library:")
    for book in books:
        print(f"{book}: ${books[book]:.2f}")
    display_dashboard()

# Create function to allow user to choose books
def choose_books():
    chosen_books = []
    total_cost = 0
    while True:
        book = input("Enter book name (type 'done' to finish choosing books): ")
        if book == "done":
            break
        elif book not in books:
            print("Invalid book name. Please try again.")
        elif book in chosen_books:
            print("You've already chosen that book. Please choose another book.")
        else:
            chosen_books.append(book)
            total_cost += books[book]
            print(f"{book} added to your list of chosen books.")
    print("You have chosen the following books:")
    for book in chosen_books:
        print(book)
    print(f"Total cost: ${total_cost:.2f}")
    display_dashboard()

# Create function to allow user to pay their bill
def pay_bill():
    total_cost = 0
    for book in chosen_books:
        total_cost += books[book]
    print(f"Your total bill is ${total_cost:.2f}")
    payment = float(input("Enter payment amount: $"))
    if payment < total_cost:
        print("Payment amount is less than total bill. Please try again.")
        pay_bill()
    else:
        change = payment - total_cost
        print(f"Payment accepted. Your change is ${change:.2f}")
        chosen_books.clear()
        display_dashboard()

# Call login function to begin
login()
