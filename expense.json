import json
import os
from datetime import datetime

DATA_FILE = "expenses.json"

def load_expenses():
    if not os.path.exists(DATA_FILE):
        return []
    with open(DATA_FILE, "r") as f:
        return json.load(f)

def save_expenses(expenses):
    with open(DATA_FILE, "w") as f:
        json.dump(expenses, f, indent=4)

def add_expense():
    try:
        amount = float(input("Amount: $"))
        category = input("Category (Food, Transport, Shopping, etc.): ").strip().title()
        description = input("Description: ").strip()
        
        expense = {
            "id": len(load_expenses()) + 1,
            "amount": amount,
            "category": category,
            "description": description,
            "date": datetime.now().strftime("%Y-%m-%d %H:%M")
        }
        
        expenses = load_expenses()
        expenses.append(expense)
        save_expenses(expenses)
        print("✅ Expense added successfully!\n")
    except ValueError:
        print("❌ Please enter a valid amount.\n")

def view_expenses():
    expenses = load_expenses()
    if not expenses:
        print("No expenses recorded yet.\n")
        return
    
    print("\n===== All Expenses =====")
    for exp in expenses:
        print(f"ID: {exp['id']} | ${exp['amount']:.2f} | {exp['category']} | {exp['description']} | {exp['date']}")
    print()

def show_summary():
    expenses = load_expenses()
    if not expenses:
        print("No expenses to summarize.\n")
        return
    
    total = sum(exp["amount"] for exp in expenses)
    categories = {}
    
    for exp in expenses:
        categories[exp["category"]] = categories.get(exp["category"], 0) + exp["amount"]
    
    print("\n===== Summary =====")
    print(f"Total spent: ${total:.2f}")
    print("\nBy Category:")
    for cat, amount in categories.items():
        print(f"  {cat}: ${amount:.2f}")
    print()

def delete_expense():
    view_expenses()
    try:
        exp_id = int(input("Enter the ID of the expense to delete: "))
        expenses = load_expenses()
        expenses = [exp for exp in expenses if exp["id"] != exp_id]
        save_expenses(expenses)
        print("✅ Expense deleted!\n")
    except ValueError:
        print("❌ Invalid ID.\n")

def main():
    while True:
        print("====== Personal Expense Tracker ======")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. Show Summary")
        print("4. Delete Expense")
        print("5. Exit")
        
        choice = input("\nChoose an option (1-5): ").strip()
        
        if choice == "1":
            add_expense()
        elif choice == "2":
            view_expenses()
        elif choice == "3":
            show_summary()
        elif choice == "4":
            delete_expense()
        elif choice == "5":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.\n")

if __name__ == "__main__":
    main()
