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
