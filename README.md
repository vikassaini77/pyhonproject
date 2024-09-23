# pyhonproject
import os

# Function to add an expense
def add_expense(expenses):
    category = input("Enter the category (e.g., Food, Transport, etc.): ")
    amount = float(input("Enter the amount spent: "))
    expenses.append((category, amount))
    print("Expense added successfully!\n")

# Function to view all expenses and total spending
def view_expenses(expenses):
    if not expenses:
        print("No expenses recorded yet.\n")
        return
    total = 0
    print("\n--- All Expenses ---")
    for idx, (category, amount) in enumerate(expenses, 1):
        print(f"{idx}. {category}: ${amount:.2f}")
        total += amount
    print(f"\nTotal Spending: ${total:.2f}\n")

# Function to save expenses to a text file
def save_expenses(expenses, filename="expenses.txt"):
    with open(filename, 'w') as file:
        for category, amount in expenses:
            file.write(f"{category},{amount}\n")
    print(f"Expenses saved to {filename}.\n")

# Function to load expenses from a text file
def load_expenses(filename="expenses.txt"):
    if not os.path.exists(filename):
        return []
    expenses = []
    with open(filename, 'r') as file:
        for line in file:
            category, amount = line.strip().split(',')
            expenses.append((category, float(amount)))
    return expenses

def main():
    expenses = load_expenses()  # Load existing expenses from file if available
    
    while True:
        print("Personal Expense Tracker")
        print("1. Add Expense")
        print("2. View All Expenses")
        print("3. Save and Exit")
        
        choice = input("Enter your choice (1-3): ")
        
        if choice == '1':
            add_expense(expenses)
        elif choice == '2':
            view_expenses(expenses)
        elif choice == '3':
            save_expenses(expenses)
            print("Exiting... Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.\n")

if __name__ == "__main__":
    main()
