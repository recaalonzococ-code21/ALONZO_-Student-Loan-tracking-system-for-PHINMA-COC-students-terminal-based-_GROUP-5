# ALONZO_-Student-Loan-tracking-system-for-PHINMA-COC-students-terminal-based-_GROUP-5
SCHOOL PURPUSES
Sample accounts
students = {"student1": "pass123"}
admins = {"admin1": "admin123"}

loans = []

# ------------------------------
# STUDENT FUNCTIONS
# ------------------------------

def apply_loan(username):
    print("\n--- APPLY FOR A LOAN ---")
    try:
        amount = float(input("Enter loan amount (â‚±): "))
        reason = input("Enter reason for loan: ")
        loans.append({
            "name": username,
            "amount": amount,
            "reason": reason,
            "status": "Pending",
            "balance": amount
        })
        print("Loan request submitted! Please wait for admin approval.\n")
    except:
        print("Invalid input. Please enter a number.\n")

def view_balance(username):
    print("\n--- YOUR LOAN RECORD ---")
    found = False
    for loan in loans:
        if loan["name"] == username:
            found = True
            print("Amount: â‚±", loan["amount"])
            print("Balance: â‚±", loan["balance"])
            print("Status:", loan["status"])
            print("Reason:", loan["reason"])
            print()
    if not found:
        print("No loan record found.\n")

def student_portal(username):
    while True:
        print("\n--- STUDENT MENU ---")
        print("[1] Apply for Loan")
        print("[2] View Loan Balance")
        print("[3] Logout")
        choice = input("Choose an option: ")

        if choice == "1":
            apply_loan(username)
        elif choice == "2":
            view_balance(username)
        elif choice == "3":
            print("Logging out...\n")
            break
        else:
            print("Invalid choice.\n")

# ------------------------------
# ADMIN FUNCTIONS
# ------------------------------

def view_loans():
    print("\n--- ALL LOAN RECORDS ---")
    if len(loans) == 0:
        print("No loan records yet.\n")
    else:
        for i, loan in enumerate(loans):
            print("Loan Number:", i + 1)
            print("Name:", loan["name"])
            print("Amount: â‚±", loan["amount"])
            print("Balance: â‚±", loan["balance"])
            print("Status:", loan["status"])
            print("Reason:", loan["reason"])
            print()

def approve_loan():
    view_loans()
    if len(loans) == 0:
        return
    try:
        num = int(input("Enter loan number to approve: "))
        index = num - 1
        if 0 <= index < len(loans):
            loans[index]["status"] = "Approved"
            print("Loan has been approved!\n")
        else:
            print("Invalid loan number.\n")
    except:
        print("Please enter a valid number.\n")

def update_payment():
    view_loans()
    if len(loans) == 0:
        return
    try:
        num = int(input("Enter loan number to update payment: "))
        index = num - 1
        if 0 <= index < len(loans):
            amount = float(input("Enter payment amount (â‚±): "))
            loans[index]["balance"] -= amount
            if loans[index]["balance"] <= 0:
                loans[index]["balance"] = 0
                loans[index]["status"] = "Paid"
            print("Payment updated!\n")
        else:
            print("Invalid loan number.\n")
    except:
        print("Please enter a valid number.\n")

def admin_portal(username):
    while True:
        print("\n--- ADMIN MENU ---")
        print("[1] View Loan Applications")
        print("[2] Approve Loan")
        print("[3] Update Payment")
        print("[4] Logout")
        choice = input("Choose an option: ")

        if choice == "1":
            view_loans()
        elif choice == "2":
            approve_loan()
        elif choice == "3":
            update_payment()
        elif choice == "4":
            print("Logging out...\n")
            break
        else:
            print("Invalid choice.\n")

# ------------------------------
# LOGIN SYSTEM
# ------------------------------

def login():
    print("=================================")
    print(" STUDENT LOAN TRACKER SYSTEM")
    print("=================================")
    print("[1] Student Login")
    print("[2] Admin Login")
    print("[3] Exit")
    choice = input("Choose your role: ")

    if choice == "1":
        username = input("Enter username: ")
        password = input("Enter password: ")
        if username in students and students[username] == password:
            print("\nWelcome,", username)
            student_portal(username)
        else:
            print("Invalid student login.\n")

    elif choice == "2":
        username = input("Enter admin username: ")
        password = input("Enter admin password: ")
        if username in admins and admins[username] == password:
            print("\nWelcome Admin,", username)
            admin_portal(username)
        else:
            print("Invalid admin login.\n")

    elif choice == "3":
        print("Exiting program... Goodbye!")
        ex
