#include <iostream>
#include <iomanip>
using namespace std;

typedef struct Student_ {

    string first_name, last_name;
    string grade;
    double quiz1, quiz2, quiz3;
    double assign1, total_marks, percentage;
    int studentId;

} Student;


Student student[100];
int studentCount = 0;
int deleteCnt = 0;
int deletedStudentId[20];

void display(void) {
    cout << "\n1- Add row/student\n2- Delete row/student\n3- Update/change row/student\n4- Insert row/student\n5- Show all rows/students\n";
}


void addStudentRow(Student &student) {

    cout << "\nEnter Student Name (FirstName, LastName): ";
    cin >> student.first_name >> student.last_name;
    cout << "Enter student Id: (0-100): ";
    cin >> student.studentId;
    cout << "Enter Student Marks Quiz1(0 to 5): ";
    cin >> student.quiz1;
    cout << "Enter Student Marks Quiz2(0 to 5): ";
    cin >> student.quiz2;
    cout << "Enter Student Marks Quiz3(0 to 5): ";
    cin >> student.quiz3;
    cout << "Enter Student Marks Assignment1(0 to 5): ";
    cin >> student.assign1;
    student.percentage = ((student.total_marks = student.quiz1 +  student.quiz2 + student.quiz3 + student.assign1) / 20) * 100;


    if(student.percentage > 89)
        student.grade = "A1";
    else if(student.percentage >= 70 && student.percentage < 89)
        student.grade = "A";
    else if(student.percentage >= 60 && student.percentage < 70)
        student.grade = "B";
    else if(student.percentage >= 50 && student.percentage < 60)
        student.grade = "C";
    else if(student.percentage >= 40 && student.percentage < 50)
        student.grade = "D";
    else if(student.percentage >= 0 && student.percentage < 40)
        student.grade = "E";
}

bool checkExistingId(Student & student, int id) {
    if(student.studentId == id)
        return true;
    
    return false;
}

void deleteStudentRow() {

    int id;
    cout << "Enter id: ";
    cin >> id;
    
    bool flag = false;
    for(int i = 0; i < studentCount; ++i) {
        flag = checkExistingId(student[i], id);
        if(flag) {
            deletedStudentId[deleteCnt++] = id;
            break;
        } 
    }

}


void updateStudentRow() {
    int stdId;
    cout << "Enter id: ";
    cin >> stdId;
    
    bool flag = false;
    for(int i = 0; i < studentCount; ++i) {
        if(checkExistingId(student[i], stdId)) {
            flag = true;        
            addStudentRow(student[i]);
            break;
        }
    }
        
    if(!flag)
        cout << "Id doesn't exist!\n";
} 
        

void insertStudentRow(Student & student) {

    cout << "\nEnter Student Name (FirstName, LastName): ";
    cin >> student.first_name >> student.last_name;
    cout << "Enter student Id: (0-100): ";
    cin >> student.studentId;
    cout << "Enter Student Marks Quiz1(0 to 5): ";
    cin >> student.quiz1;
    cout << "Enter Student Marks Quiz2(0 to 5): ";
    cin >> student.quiz2;
    cout << "Enter Student Marks Quiz3(0 to 5): ";
    cin >> student.quiz3;
    cout << "Enter Student Marks Assignment1(0 to 5): ";
    cin >> student.assign1;
    student.percentage = ((student.total_marks = student.quiz1 +  student.quiz2 + student.quiz3 + student.assign1) / 20) * 100;


    if(student.percentage > 89)
        student.grade = "A1";
    else if(student.percentage >= 70 && student.percentage < 89)
        student.grade = "A";
    else if(student.percentage >= 60 && student.percentage < 70)
        student.grade = "B";
    else if(student.percentage >= 50 && student.percentage < 60)
        student.grade = "C";
    else if(student.percentage >= 40 && student.percentage < 50)
        student.grade = "D";
    else if(student.percentage >= 0 && student.percentage < 40)
        student.grade = "E";

}


void showStudentRows() {

    cout << "\nStudent Name   |   Student ID  | Quiz 1 | Quiz 2 | Quiz 3 | Assign | Total Marks | Percentage | Grades\n";
    cout << "----------------------------------------------------------------------------------------------------\n";

    for(int j = 0; j < studentCount; j++) {
        int tmp = 0;
            if(!checkExistingId(student[j], deletedStudentId[tmp])) {
                cout << student[j].first_name <<' '<< student[j].last_name << setw(12) << student[j].studentId << setw(8) << student[j].quiz1 << setw(8) << student[j].quiz2
                    << setw(8) << student[j].quiz3 << setw(8) << student[j].assign1 << setw(12) << student[j].total_marks << setw(12) << student[j].percentage
                    << setw(8) << student[j].grade << endl;
                tmp++;
            
        }
    }
}




int main(void) {

    int choice;
    char exit;
    
    do{
        do {
            display();
            cout << "\nEnter choice: ";
            cin >> choice;
        } while(!(choice > 0 && choice < 6));

        switch (choice)
        {
        case 1:
            addStudentRow(student[studentCount++]);
            cout << "\n====================================================\n";
            break;
        
        case 2:
            deleteStudentRow();
            cout << "Student Row Successfully Deleted!\n";
            cout << "\n====================================================\n";
            break;

        case 3:
            updateStudentRow();
            cout << "\n====================================================\n";
            break;
        
        case 4:
            insertStudentRow(student[studentCount++]);
            cout << "\n====================================================\n";
            break;

        case 5:
            showStudentRows();
            cout << "\n====================================================\n";
            break;

        default:
            break;
        }

        cout << "Are you want to quit (y/n): ";
        cin >> exit;
    } while(!(exit == 'y' || exit == 'Y'));

    cout << "\nTHANK YOU :)\n";
    return 0;
}
