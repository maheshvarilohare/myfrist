import json
import os

# Load or initialize data
if os.path.exists("data.json"):
    with open("data.json", "r") as f:
        db = json.load(f)
else:
    db = {"students": {}, "courses": {}, "enrollments": {}}

# Save data
def save():
    with open("data.json", "w") as f:
        json.dump(db, f, indent=4)

def add_student():
    sid = input("Enter student ID: ")
    name = input("Enter student name: ")
    db["students"][sid] = {"name": name}
    save()
    print("Student added.")

def add_course():
    cid = input("Enter course ID: ")
    cname = input("Enter course name: ")
    db["courses"][cid] = {"name": cname}
    save()
    print("Course added.")

def enroll_student():
    sid = input("Enter student ID: ")
    cid = input("Enter course ID: ")
    if sid in db["students"] and cid in db["courses"]:
        db["enrollments"].setdefault(sid, []).append(cid)
        save()
        print("Enrollment successful.")
    else:
        print("Invalid student or course ID.")

def view_students():
    print("\nStudents:")
    for sid, info in db["students"].items():
        print(f"{sid}: {info['name']}")

def view_courses():
    print("\nCourses:")
    for cid, info in db["courses"].items():
        print(f"{cid}: {info['name']}")

def view_enrollments():
    print("\nEnrollments:")
    for sid, courses in db["enrollments"].items():
        student_name = db["students"][sid]["name"]
        course_names = [db["courses"][cid]["name"] for cid in courses]
        print(f"{student_name} ({sid}) enrolled in: {', '.join(course_names)}")

# Menu
def main():
    while True:
        print("\n--- University Management System ---")
        print("1. Add Student")
        print("2. Add Course")
        print("3. Enroll Student in Course")
        print("4. View Students")
        print("5. View Courses")
        print("6. View Enrollments")
        print("0. Exit")
        choice = input("Enter your choice: ")

        if choice == "1":
            add_student()
        elif choice == "2":
            add_course()
        elif choice == "3":
            enroll_student()
        elif choice == "4":
            view_students()
        elif choice == "5":
            view_courses()
        elif choice == "6":
            view_enrollments()
        elif choice == "0":
            break
        else:
            print("Invalid choice.")

main()













