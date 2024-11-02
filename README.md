#include <iostream>
#include <vector>
#include <iomanip>
#include <limits>
 
struct Student {
   int id;
   std::string name;
   int age;
   std::string major;
};
 
class StudentDatabase {
public:
   void addStudent() {
       Student student;
       student.id = nextId++;
       std::cout << "Enter name: ";
       std::cin.ignore();
       std::getline(std::cin, student.name);
       std::cout << "Enter age: ";
       std::cin >> student.age;
       std::cout << "Enter major: ";
       std::cin.ignore();
       std::getline(std::cin, student.major);
       students.push_back(student);
       std::cout << "Student added with ID: " << student.id << "\n";
   }
 
   void viewStudents() const {
       if (students.empty()) {
           std::cout << "No students in the database.\n";
           return;
       }
       std::cout << std::left << std::setw(10) << "ID"
                 << std::setw(20) << "Name"
                 << std::setw(5) << "Age"
                 << std::setw(20) << "Major" << "\n";
       std::cout << std::string(55, '-') << "\n";
       for (const auto& student : students) {
           std::cout << std::left << std::setw(10) << student.id
                     << std::setw(20) << student.name
                     << std::setw(5) << student.age
                     << std::setw(20) << student.major << "\n";
       }
   }
 
   void updateStudent() {
       int id;
       std::cout << "Enter student ID to update: ";
       std::cin >> id;
 
       for (auto& student : students) {
           if (student.id == id) {
               std::cout << "Updating student: " << student.name << "\n";
               std::cout << "Enter new name: ";
               std::cin.ignore();
               std::getline(std::cin, student.name);
               std::cout << "Enter new age: ";
               std::cin >> student.age;
               std::cout << "Enter new major: ";
               std::cin.ignore();
               std::getline(std::cin, student.major);
               std::cout << "Student updated.\n";
               return;
           }
       }
       std::cout << "Student ID not found.\n";
   }
 
   void deleteStudent() {
       int id;
       std::cout << "Enter student ID to delete: ";
       std::cin >> id;
 
       for (auto it = students.begin(); it != students.end(); ++it) {
           if (it->id == id) {
               students.erase(it);
               std::cout << "Student with ID " << id << " deleted.\n";
               return;
           }
       }
       std::cout << "Student ID not found.\n";
   }
 
private:
   std::vector<Student> students;
   int nextId = 1;
};
 
void showMenu() {
   std::cout << "\n--- Student Database Management System ---\n";
   std::cout << "1. Add Student\n";
   std::cout << "2. View Students\n";
   std::cout << "3. Update Student\n";
   std::cout << "4. Delete Student\n";
   std::cout << "5. Exit\n";
   std::cout << "Select an option: ";
}
 
int main() {
   StudentDatabase db;
   int choice;
 
   while (true) {
       showMenu();
       std::cin >> choice;
 
       switch (choice) {
           case 1:
               db.addStudent();
               break;
           case 2:
               db.viewStudents();
               break;
           case 3:
               db.updateStudent();
               break;
           case 4:
               db.deleteStudent();
               break;
           case 5:
               std::cout << "Exiting the program.\n";
               return 0;
           default:
               std::cout << "Invalid option. Please try again.\n";
               break;
       }
   }
 
   return 0;
}
