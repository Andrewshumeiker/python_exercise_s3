# python_exercise_s3
This repository is to show the 10 Python exercises that were placed in week 3, along with these is a readme about the object-oriented programming paradigm.
## library Book Tracker
```python
library = []

def add_book():
    title = input("Book title: ").strip()
    author = input("Author: ").strip()
    try:
        pages = int(input("Number of pages: "))
        library.append({"title": title, "author": author, "pages": pages})
        print("Book added successfully.")
    except ValueError:
        print("Invalid number of pages.")

def search_book():
    query = input("Search by title: ").strip().lower()
    results = [book for book in library if query in book["title"].lower()]
    if results:
        print("\n--- Search Results ---")
        for book in results:
            print(f"{book['title']} - {book['author']} ({book['pages']} pages)")
    else:
        print("No books found.")

def show_all_books():
    if library:
        print("\n--- ALL BOOKS IN LIBRARY ---")
        for book in library:
            print(f"{book['title']} - {book['author']} ({book['pages']} pages)")
    else:
        print("Library is empty.")

def library_menu():
    while True:
        print("\n--- VIRTUAL LIBRARY ---")
        print("1. Add book")
        print("2. Search book")
        print("3. Show all books")
        print("0. Exit")

        choice = input("Choose an option: ").strip()
        if choice == "1":
            add_book()
        elif choice == "2":
            search_book()
        elif choice == "3":
            show_all_books()
        elif choice == "0":
            break
        else:
            print("Invalid option.")
library_menu()
```
## Student Grade manager
```python
students = {}

def add_student():
    name = input("Student name: ").strip()
    if name in students:
        print("Student already exists.")
    else:
        students[name] = []
        print("Student added.")

def record_grade():
    name = input("Student name: ").strip()
    if name not in students:
        print("Student not found.")
        return
    try:
        grade = float(input("Enter grade: "))
        students[name].append(grade)
        print("Grade recorded.")
    except ValueError:
        print("Invalid grade.")

def show_average():
    name = input("Student name: ").strip()
    if name in students and students[name]:
        avg = sum(students[name]) / len(students[name])
        print(f"Average grade for {name}: {avg:.2f}")
    else:
        print("Student not found or no grades available.")

def student_menu():
    while True:
        print("\n--- STUDENT GRADE MANAGER ---")
        print("1. Add student")
        print("2. Record grade")
        print("3. Show average grade")
        print("0. Exit")

        choice = input("Choose an option: ").strip()
        if choice == "1":
            add_student()
        elif choice == "2":
            record_grade()
        elif choice == "3":
            show_average()
        elif choice == "0":
            break
        else:
            print("Invalid option.")
student_menu()
```
## Restaurant menu editor
```python
menu = []

def add_dish():
    name = input("Dish name: ").strip()
    try:
        price = float(input("Price: "))
        available = input("Is it available? (yes/no): ").strip().lower() == "yes"
        menu.append({"name": name, "price": price, "available": available})
        print("Dish added.")
    except ValueError:
        print("Invalid price.")

def update_availability():
    name = input("Dish name: ").strip().lower()
    for dish in menu:
        if dish["name"].lower() == name:
            dish["available"] = not dish["available"]
            print("Availability updated.")
            return
    print("Dish not found.")

def count_available_dishes():
    count = sum(1 for dish in menu if dish["available"])
    print(f"Total available dishes: {count}")

def restaurant_menu():
    while True:
        print("\n--- RESTAURANT MENU EDITOR ---")
        print("1. Add dish")
        print("2. Toggle availability")
        print("3. Count available dishes")
        print("0. Exit")

        choice = input("Choose an option: ").strip()
        if choice == "1":
            add_dish()
        elif choice == "2":
            update_availability()
        elif choice == "3":
            count_available_dishes()
        elif choice == "0":
            break
        else:
            print("Invalid option.")
restaurant_menu()
```
## Warehouse Box counter
```python
warehouse = {}

def add_box_type():
    box = input("Box type: ").strip()
    try:
        quantity = int(input("Quantity: "))
        if quantity < 0:
            print("Quantity cannot be negative.")
            return
        warehouse[box] = warehouse.get(box, 0) + quantity
        print("Box type added/updated.")
    except ValueError:
        print("Invalid quantity.")

def update_quantity():
    box = input("Box type to update: ").strip()
    if box in warehouse:
        try:
            new_qty = int(input("New quantity: "))
            if new_qty < 0:
                print("Quantity cannot be negative.")
            else:
                warehouse[box] = new_qty
                print("Quantity updated.")
        except ValueError:
            print("Invalid input.")
    else:
        print("Box type not found.")

def check_quantity():
    box = input("Box type to check: ").strip()
    if box in warehouse:
        print(f"Quantity of '{box}': {warehouse[box]}")
    else:
        print("Box type not found.")

def warehouse_menu():
    while True:
        print("\n--- WAREHOUSE BOX COUNTER ---")
        print("1. Add box type")
        print("2. Update quantity")
        print("3. Check quantity")
        print("0. Exit")

        choice = input("Choose an option: ").strip()
        if choice == "1":
            add_box_type()
        elif choice == "2":
            update_quantity()
        elif choice == "3":
            check_quantity()
        elif choice == "0":
            break
        else:
            print("Invalid option.")
warehouse_menu()
```
## Movie rating system
```python
movies = []
# Add a new movie to the list
def add_movie():
    title = input("Enter the movie title: ").strip()
    if not title:
        print("Title cannot be empty.")
        return
    for movie in movies:
        if movie['title'].lower() == title.lower():
            print("This movie already exists.")
            return
    movies.append({'title': title, 'ratings': []})
    print(f"Movie '{title}' added successfully.")

# Register a rating for a movie
def rate_movie():
    if not movies:
        print("No movies available.")
        return
    title = input("Enter the movie title to rate: ").strip()
    for movie in movies:
        if movie['title'].lower() == title.lower():
            try:
                rating = int(input("Enter rating (1–5): "))
                if 1 <= rating <= 5:
                    movie['ratings'].append(rating)
                    print("Rating added successfully.")
                else:
                    print("Rating must be between 1 and 5.")
            except ValueError:
                print("Please enter a valid number.")
            return
    print("Movie not found.")

# Show average rating for each movie
def show_ratings():
    if not movies:
        print("No movies registered yet.")
        return
    for movie in movies:
        title = movie['title']
        ratings = movie['ratings']
        if ratings:
            avg = sum(ratings) / len(ratings)
            print(f"{title}: Average rating = {avg:.2f}")
        else:
            print(f"{title}: No ratings yet.")

# User menu
def movie_menu():
    while True:
        print("\n--- Movie Rating System ---")
        print("1. Add movie")
        print("2. Rate a movie")
        print("3. Show average ratings")
        print("4. Exit")
        choice = input("Choose an option: ")
        if choice == "1":
            add_movie()
        elif choice == "2":
            rate_movie()
        elif choice == "3":
            show_ratings()
        elif choice == "4":
            print("Exiting...")
            break
        else:
            print("Invalid option. Try again.")
movie_menu()
```
## Online course tracker
```python
courses = []

def add_course():
    title = input("Course title: ").strip()
    try:
        duration = int(input("Duration (hours): "))
        enrolled = int(input("Number of students enrolled: "))
        if duration < 0 or enrolled < 0:
            raise ValueError
    except ValueError:
        print("Invalid input.")
        return
    courses.append({'title': title, 'duration': duration, 'enrolled': enrolled})
    print(f"Course '{title}' added.")

def update_enrollment():
    title = input("Course to update: ").strip()
    for course in courses:
        if course['title'].lower() == title.lower():
            try:
                enrolled = int(input("New number of students: "))
                if enrolled < 0:
                    raise ValueError
                course['enrolled'] = enrolled
                print("Enrollment updated.")
            except ValueError:
                print("Invalid number.")
            return
    print("Course not found.")

def filter_by_duration():
    try:
        min_duration = int(input("Minimum duration (hours): "))
        for course in courses:
            if course['duration'] >= min_duration:
                print(f"{course['title']} - {course['duration']} hours")
    except ValueError:
        print("Invalid duration.")

def course_menu():
    while True:
        print("\n--- Course Tracker ---")
        print("1. Add Course")
        print("2. Update Enrollment")
        print("3. Filter by Duration")
        print("4. Exit")
        opt = input("Choose: ")
        if opt == "1":
            add_course()
        elif opt == "2":
            update_enrollment()
        elif opt == "3":
            filter_by_duration()
        elif opt == "4":
            break
        else:
            print("Invalid option.")
course_menu()
```
## To do list organizer
```python
tasks = []

def add_task():
    desc = input("Task description: ").strip()
    priority = input("Priority (low/medium/high): ").lower()
    tasks.append({'desc': desc, 'priority': priority, 'done': False})
    print("Task added.")

def mark_done():
    desc = input("Task to mark as done: ").strip()
    for task in tasks:
        if task['desc'].lower() == desc.lower():
            task['done'] = True
            print("Marked as completed.")
            return
    print("Task not found.")

def filter_tasks():
    print("1. Filter by priority")
    print("2. Filter by status")
    opt = input("Choose: ")
    if opt == "1":
        level = input("Priority level: ").lower()
        for task in tasks:
            if task['priority'] == level:
                print(task)
    elif opt == "2":
        status = input("Status (done/pending): ").lower()
        for task in tasks:
            if (status == "done" and task['done']) or (status == "pending" and not task['done']):
                print(task)

def todo_menu():
    while True:
        print("\n--- To-Do List ---")
        print("1. Add Task")
        print("2. Mark as Done")
        print("3. Filter Tasks")
        print("4. Exit")
        opt = input("Choose: ")
        if opt == "1":
            add_task()
        elif opt == "2":
            mark_done()
        elif opt == "3":
            filter_tasks()
        elif opt == "4":
            break
todo_menu()
```
## Digital wallet
```python
expenses = []

def add_expense():
    category = input("Category: ").strip()
    try:
        amount = float(input("Amount: "))
        if amount < 0:
            raise ValueError
        expenses.append({'category': category, 'amount': amount})
        print("Expense recorded.")
    except ValueError:
        print("Invalid amount.")

def total_expenses():
    total = sum(e['amount'] for e in expenses)
    print(f"Total spent: ${total:.2f}")

def category_percentages():
    total = sum(e['amount'] for e in expenses)
    if total == 0:
        print("No expenses.")
        return
    categories = {}
    for e in expenses:
        categories[e['category']] = categories.get(e['category'], 0) + e['amount']
    for cat, amt in categories.items():
        print(f"{cat}: {amt / total * 100:.2f}%")

def wallet_menu():
    while True:
        print("\n--- Digital Wallet ---")
        print("1. Add Expense")
        print("2. Total Expenses")
        print("3. Category Percentages")
        print("4. Exit")
        opt = input("Choose: ")
        if opt == "1":
            add_expense()
        elif opt == "2":
            total_expenses()
        elif opt == "3":
            category_percentages()
        elif opt == "4":
            break
wallet_menu()
```
## Pet adoption center
```python
pets = []

def add_pet():
    name = input("Name: ").strip()
    species = input("Species: ").strip()
    try:
        age = int(input("Age: "))
        if age < 0:
            raise ValueError
        pets.append({'name': name, 'species': species, 'age': age})
        print("Pet added.")
    except ValueError:
        print("Invalid age.")

def search_species():
    specie = input("Species to search: ").strip()
    for pet in pets:
        if pet['species'].lower() == specie.lower():
            print(pet)

def filter_by_age():
    try:
        max_age = int(input("Max age: "))
        for pet in pets:
            if pet['age'] <= max_age:
                print(pet)
    except ValueError:
        print("Invalid age.")

def pet_menu():
    while True:
        print("\n--- Pet Adoption Center ---")
        print("1. Add Pet")
        print("2. Search by Species")
        print("3. Filter by Age")
        print("4. Exit")
        opt = input("Choose: ")
        if opt == "1":
            add_pet()
        elif opt == "2":
            search_species()
        elif opt == "3":
            filter_by_age()
        elif opt == "4":
            break
pet_menu()
```
## Gym membership system
```python
members = []
def register_member(name, plan):
    if not name.strip():
        raise ValueError("Name cannot be empty.")
    if plan.lower() not in ["monthly", "quarterly", "yearly"]:
        raise ValueError("Invalid plan. Use: monthly, quarterly, or yearly.")
    
    members.append({
        "name": name.strip(),
        "plan": plan.lower(),
        "is_up_to_date": True
    })
    print(f"Member '{name}' registered with plan '{plan}'.")
def change_plan(name, new_plan):
    for member in members:
        if member["name"].lower() == name.lower():
            if new_plan.lower() not in ["monthly", "quarterly", "yearly"]:
                raise ValueError("Invalid plan. Use: monthly, quarterly, or yearly.")
            member["plan"] = new_plan.lower()
            print(f"Plan for '{name}' updated to '{new_plan}'.")
            return
    raise ValueError("Member not found.")
def mark_as_overdue(name):
    for member in members:
        if member["name"].lower() == name.lower():
            member["is_up_to_date"] = False
            print(f"Member '{name}' marked as overdue.")
            return
    raise ValueError("Member not found.")
def mark_as_up_to_date(name):
    for member in members:
        if member["name"].lower() == name.lower():
            member["is_up_to_date"] = True
            print(f"Member '{name}' is now up-to-date with payment.")
            return
    raise ValueError("Member not found.")
def list_overdue_members():
    overdue = [m for m in members if not m["is_up_to_date"]]
    if overdue:
        print("\n--- Members with overdue payments ---")
        for m in overdue:
            print(f"{m['name']} ({m['plan']})")
    else:
        print("All members are up-to-date.")
def gym_menu():
    while True:
        print("\n--- Gym Membership System ---")
        print("1. Register new member")
        print("2. Change membership plan")
        print("3. Mark payment as overdue")
        print("4. Mark payment as up-to-date")
        print("5. List members with overdue payments")
        print("6. Exit")
        
        choice = input("Choose an option: ")
        
        try:
            if choice == "1":
                name = input("Member name: ")
                plan = input("Plan (monthly/quarterly/yearly): ")
                register_member(name, plan)
            elif choice == "2":
                name = input("Member name: ")
                new_plan = input("New plan (monthly/quarterly/yearly): ")
                change_plan(name, new_plan)
            elif choice == "3":
                name = input("Member name to mark as overdue: ")
                mark_as_overdue(name)
            elif choice == "4":
                name = input("Member name to mark as up-to-date: ")
                mark_as_up_to_date(name)
            elif choice == "5":
                list_overdue_members()
            elif choice == "6":
                print("Exiting the system...")
                break
            else:
                print("Invalid option.")
        except ValueError as e:
            print(f"Error: {e}")
gym_menu()
```
