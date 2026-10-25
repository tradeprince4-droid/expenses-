
import json
import os
from datetime import datetime

FILE = "expenses.json"


def load_expenses():
    if os.path.exists(FILE):
        with open(FILE, "r") as file:
            return json.load(file)
    return []


def save_expenses(expenses):
    with open(FILE, "w") as file:
        json.dump(expenses, file, indent=4)


def add_expense(expenses):
    title = input("Expense name: ").strip()
    category = input("Category: ").strip()

    try:
        amount = float(input("Amount (₹): "))
        if amount <= 0:
            print("Amount must be greater than zero.")
            return
    except ValueError:
        print("Please enter a valid amount.")
        return

    expense = {
        "title": title,
        "category": category,
        "amount": amount,
        "date": datetime.now().strftime("%Y-%m-%d %H:%M")
    }

    expenses.append(expense)
    save_expenses(expenses)
    print("Expense saved successfully!")


def view_expenses(expenses):
    if not expenses:
        print("No expenses recorded yet.")
        return

    print("\n--- EXPENSE HISTORY ---")
    for number, expense in enumerate(expenses, start=1):
        print(
            f"{number}. {expense['title']} | "
            f"{expense['category']} | "
            f"₹{expense['amount']:.2f} | "
            f"{expense['date']}"
        )


def show_summary(expenses):
    total = sum(item["amount"] for item in expenses)
    print(f"\nTotal expenses: ₹{total:.2f}")

    categories = {}
    for item in expenses:
        category = item["category"]
        categories[category] = (
            categories.get(category, 0) + item["amount"]
        )

    if categories:
        print("\nSpending by category:")
        for category, amount in categories.items():
            print(f"{category}: ₹{amount:.2f}")


def main():
    expenses = load_expenses()

    while True:
        print("\n=== NEON EXPENSE TRACKER ===")
        print("1. Add expense")
        print("2. View expenses")
        print("3. Spending summary")
        print("4. Exit")

        choice = input("Choose an option: ").strip()

        if choice == "1":
            add_expense(expenses)
        elif choice == "2":
            view_expenses(expenses)
        elif choice == "3":
            show_summary(expenses)
        elif choice == "4":
            print("Thank you for using Neon Expense Tracker!")
            break
        else:
            print("Invalid choice. Try again.")


if __name__ == "__main__":
    main()
    
# ⚡ Neon Expense Tracker

A simple Python project to manage personal expenses.

## Features
- Add daily expenses
- View expense history
- Calculate total spending
- Group expenses by category
- Automatically save data in JSON format
- Simple command-line interface

## Technologies
- Python 3
- JSON
- Datetime module

## How to Run

1. Install Python 3.
2. Download or clone this repository.
3. Open a terminal in the project folder.
4. Run:

   ```bash
   python expense_tracker.py
   ```

## Project Structure

```text
expense-tracker/
├── expense_tracker.py
├── expenses.json
└── README.md
```

The `expenses.json` file is created automatically
when you save your first expense.

## License
MIT
# expenses-
