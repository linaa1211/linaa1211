#include <iostream>
#include <vector>
#include <string>

using namespace std;

struct Student{
    string name; 
    vector<string> predmet; 
    vector<vector<int>> grades; 
};

int main(){
    vector<Student> students; 
    int choice;

    while (true){
        cout << "\nЕлектронний Щоденник\n";
        cout << "1. Додати учня\n";
        cout << "2. Додати оцінку\n";
        cout << "3. Переглянути оцінки учня\n";
        cout << "4. Переглянути середній бал учня\n";
        cout << "5. Вийти\n";
        cout << "Виберіть дію: ";
        cin >> choice;

        if (choice == 1) {
            string studentName;
            cout << "Введіть ім'я учня: ";
            cin.ignore();
            getline(cin, studentName);

            Student newStudent;
            newStudent.name = studentName;
            students.push_back(newStudent);
            cout << "Учень " << studentName << " доданий!\n";

        }
        else if (choice == 2){
          string studentName, subject;
            int grade;
            bool found = false;

            cout << "Введіть ім'я учня: ";
            cin.ignore();
            getline(cin, studentName);

            for (auto& student : students) {
                if (student.name == studentName) {
                    found = true;
                    cout << "Введіть предмет: ";
                    getline(cin, subject);
                    cout << "Введіть оцінку: ";
                    cin >> grade;

                    student.predmet.push_back(subject);
                    student.grades.push_back({grade});
                    cout << "Оцінка " << grade << " додана до предмета " << subject << ".\n";
                    break;
                }
            }

            if (!found){
                cout << "Учень не знайдений!\n";
            }
        } 
        else if (choice == 3){
            string studentName;
            bool found = false;

            cout << "Введіть ім'я учня: ";
            cin.ignore(); 
            getline(cin, studentName);

            for (const auto& student : students){
                if (student.name == studentName){
                    found = true;
                    cout << "Оцінки учня " << studentName << ":\n";
                    for (size_t i = 0; i < student.predmet.size(); i++){
                        cout << student.predmet[i] << ": ";
                        for (int grade : student.grades[i]){
                            cout << grade << " ";
                        }
                        cout << endl;
                    }
                    break;
                }
            }

            if (!found) {
                cout << "Учень не знайдений!\n";
            }
        } 
        else if (choice == 4){
            string studentName;
            bool found = false;

            cout << "Введіть ім'я учня: ";
            cin.ignore();
            getline(cin, studentName);

            for (const auto& student : students){
                if (student.name == studentName){
                    found = true;  
                    double totalSum = 0;
                    int count = 0;
                    for (const auto& gradesList : student.grades){
                        for (int grade : gradesList){
                            totalSum += grade;
                            count;
                        }
                    }
                    if (count > 0){
                        cout << "Середній бал учня " << studentName << ": " << totalSum / count << endl;
                    } 
                    else {
                        cout << "У учня немає оцінок.\n";
                    }
                    break;
                }
            }

            if (!found) {
                cout << "Учень не знайдений!\n";
            }
        } 
        else if (choice == 5){
            cout << "До побачення!\n";
            break;
        } 
        else{
            cout << "Невірний вибір. Спробуйте ще раз.\n";
        }
    }
}
