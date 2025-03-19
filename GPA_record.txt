#include <iostream>
#include <cstring>
using namespace std;

struct Student {
    int id;
    char firstName[50], lastName[50], course[50];
    float prevGPA;
};

const int MAX_STUDENTS = 5;
Student students[MAX_STUDENTS];
int studentCount = 0;

void addStudent() {
    system("cls");
    if (studentCount >= MAX_STUDENTS) {
        cout << "Student list is full!\n";
        return;
    }
    Student s;
    cout << "Enter Student ID: ";
    cin >> s.id;

    for (int i = 0; i < studentCount; i++) {
        if (students[i].id == s.id) {
            cout << "Student ID already exists!\n";
            return;
        }
    }
    cout << "Enter First Name: ";
    cin >> s.firstName;
    cout << "Enter Last Name: ";
    cin >> s.lastName;
    cout << "Enter Course: ";
    cin >> s.course;
    cout << "Enter Previous Semestral GPA: ";
    cin >> s.prevGPA;

    students[studentCount++] = s;
    cout << "Student added successfully!\n";
}

void editStudent() {
    system("cls");
    if (studentCount == 0) {
        cout << "No students to edit!\n";
        return;
    }
    int id;
    cout << "Enter Student ID to edit: ";
    cin >> id;
    for (int i = 0; i < studentCount; i++) {
        if (students[i].id == id) {
            cout << "Editing student: " << students[i].firstName << " " << students[i].lastName << "\n";
            cout << "Enter New First Name: ";
            cin >> students[i].firstName;
            cout << "Enter New Last Name: ";
            cin >> students[i].lastName;
            cout << "Enter New Course: ";
            cin >> students[i].course;
            cout << "Enter New GPA: ";
            cin >> students[i].prevGPA;
            cout << "Student updated successfully!\n";
            return;
        }
    }
    cout << "Student not found!\n";
}

void deleteStudent() {
    system("cls");
    if (studentCount == 0) {
        cout << "No students to delete!\n";
        return;
    }
    int id;
    cout << "Enter Student ID to delete: ";
    cin >> id;
    for (int i = 0; i < studentCount; i++) {
        if (students[i].id == id) {
            for (int j = i; j < studentCount - 1; j++) {
                students[j] = students[j + 1];
            }
            studentCount--;
            cout << "Student deleted successfully!\n";
            return;
        }
    }
    cout << "Student not found!\n";
}

void viewStudents() {
    system("cls");
    if (studentCount == 0) {
        cout << "No students to display!\n";
        return;
    }
    cout << "View Options:\n1. Alphabetically\n2. By GPA\nSelect option: ";
    int option;
    cin >> option;
    if (option == 1) {
        for (int i = 0; i < studentCount - 1; i++) {
            for (int j = i + 1; j < studentCount; j++) {
                if (strcmp(students[i].lastName, students[j].lastName) > 0) {
                    swap(students[i], students[j]);
                }
            }
        }
    } else if (option == 2) {
        for (int i = 0; i < studentCount - 1; i++) {
            for (int j = i + 1; j < studentCount; j++) {
                if (students[i].prevGPA > students[j].prevGPA) {
                    swap(students[i], students[j]);
                }
            }
        }
    } else {
        cout << "Invalid option!\n";
        return;
    }
    cout << "\nID\tName\tCourse\tGPA\n";
    for (int i = 0; i < studentCount; i++) {
        cout << students[i].id << "\t" << students[i].firstName << " " << students[i].lastName << "\t" << students[i].course << "\t" << students[i].prevGPA << "\n";
    }
}

int main() {
    int choice;
    do {
        system("cls");
        cout << "\nMenu:\n1. Add Student\n2. Edit Student\n3. Delete Student\n4. View Students\n5. Exit\nSelect option: ";
        cin >> choice;
        switch (choice) {
            case 1: addStudent(); break;
            case 2: editStudent(); break;
            case 3: deleteStudent(); break;
            case 4: viewStudents(); break;
            case 5: cout << "Exiting program...\n"; break;
            default: cout << "Invalid option!\n";
        }
    } while (choice != 5);
    return 0;
}
