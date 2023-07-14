# Gread_book_Management_System_
class Student:
    def __init__(self, name):
        self.name = name
        self.marks = {}

    def add_mark(self, subject, mark):
        self.marks[subject] = mark

    def calculate_percentage(self, total_marks):
        if total_marks != 0:
            return (sum(self.marks.values()) / total_marks) * 100
        else:
            return 0

    def determine_status(self, total_marks):
        percentage = self.calculate_percentage(total_marks)
        if percentage >= 50:
            return "Pass"
        else:
            return "Fail"

    def calculate_grade(self, total_marks):
        percentage = self.calculate_percentage(total_marks)
        if percentage >= 90:
            return "A+"
        elif percentage >= 80:
            return "A"
        elif percentage >= 70:
            return "B"
        elif percentage >= 60:
            return "C"
        elif percentage >= 35:
            return "D"
        else:
            return "F"


class Gradebook:
    def __init__(self):
        self.students = []
        self.subjects = []
        self.total_marks = {}

    def set_subjects(self, subjects):
        self.subjects = subjects

    def set_total_marks(self):
        for subject in self.subjects:
            total_mark = float(input(f"Enter the total marks for {subject}: "))
            self.total_marks[subject] = total_mark

    def add_student(self, student):
        self.students.append(student)

    def input_student_grades(self):
        for student in self.students:
            print(f"\nEnter marks for {student.name}:")
            for subject in self.subjects:
                total_marks = self.total_marks[subject]
                while True:
                    mark = float(input(f"Enter marks for {subject}: "))
                    if mark <= total_marks:
                        student.add_mark(subject, mark)
                        break
                    else:
                        print("Entered marks exceed the total marks. Please enter a valid value.")

    def generate_percentage_report(self):
        print("\nPercentage Report:")
        for student in self.students:
            total_marks_obtained = sum(student.marks.values())
            status = student.determine_status(sum(self.total_marks.values()))
            grade = student.calculate_grade(sum(self.total_marks.values()))
            percentage = student.calculate_percentage(sum(self.total_marks.values()))
            print(f"{student.name}: Total Marks Obtained = {total_marks_obtained:.2f}, Percentage = {percentage:.2f}%, Status = {status}, Grade = {grade}")


# Create the gradebook object
gradebook = Gradebook()

# Get the subjects from the user
subjects = input("Enter the subjects separated by spaces: ").split()
gradebook.set_subjects(subjects)

# Set total marks for each subject
gradebook.set_total_marks()

# Create students and add them to the gradebook
num_students = int(input("Enter the number of students: "))
for i in range(num_students):
    student_name = input(f"\nEnter the name of student {i + 1}: ")
    student = Student(student_name)
    gradebook.add_student(student)

# Input marks for each student and subject
gradebook.input_student_grades()

# Generate percentage report
gradebook.generate_percentage_report()
