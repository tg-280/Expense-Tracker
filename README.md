# Expense-Tracker
A simple clean app for keeping track of expenses.
Author - Tiya Gupta

import csv
from datetime import datetime

FILENAME = "expenses.csv"

def add_expense():
    amount = float(input("Enter expense amount: ₹"))
    category = input("Enter category (Food, Travel, etc.): ")
    note = input("Enter a short note: ")
    date = datetime.now().strftime("%Y-%m-%d")

    with open(FILENAME, mode="a", newline="") as file:
        writer = csv.writer(file)
        writer.writerow([date, category, amount, note])

    print("✅ Expense added successfully!\n")
def view_expenses():
    try:
        with open(FILENAME, mode="r") as file:
            reader = csv.reader(file)
            print("\n📋 All Expenses:")
            for row in reader:
                print(f"📅 {row[0]} | 📂 {row[1]} | 💸 ₹{row[2]} | 📝 {row[3]}")
    except FileNotFoundError:
        print("No expenses found yet.\n")

def show_summary():
    totals = {}
    try:
        with open(FILENAME, mode="r") as file:
            reader = csv.reader(file)
            for row in reader:
                category = row[1]
                amount = float(row[2])
                totals[category] = totals.get(category, 0) + amount

        print("\n📊 Category-wise Summary:")
        for category, total in totals.items():
            print(f"{category}: ₹{total}")
    except FileNotFoundError:
        print("No data to summarize.\n")

def menu():
    while True:
        print("\n----- Expense Tracker Menu -----")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. View Summary")
        print("4. Exit")
        choice = input("Choose an option (1-4): ")

        if choice == "1":
            add_expense()
        elif choice == "2":
            view_expenses()
        elif choice == "3":
            show_summary()
        elif choice == "4":
            print("Goodbye! 👋")
            break
        else:
            print("Invalid option. Please choose 1–4.\n")

# Run the app
menu()

