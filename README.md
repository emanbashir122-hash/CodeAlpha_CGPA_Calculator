# CodeAlpha_CGPA_Calculator

#include <iostream>/>
#include <string>/>
#include <vector>/>
#include <iomanip> // decimal ke liye/>
using namespace std;/>

double gradeToPoint(char g) />
{/>
    if(g=='A'||g=='a') return 4.0;/>
    if(g=='B'||g=='b') return 3.0;/>
    if(g=='C'||g=='c') return 2.0;/>
    if(g=='D'||g=='d') return 1.0;/>
    if(g=='F'||g=='f') return 0.0;/>
    return -1; // invalid grade/>
}/>

int main()/>
{/>
    int n;/>
    cout << "=== CodeAlpha Task 1: CGPA Calculator ===\n";/>
    cout << "Kitne courses liye hain is semester: ";/>
    cin >> n;/>

    vector<string> course(n);/>
    vector<char> grade(n);
    vector<double> credit(n);

    double totalCredit = 0, totalGradePoints = 0;

    cout << "\n--- Har course ka data daalo ---\n";
    for(int i=0; i<n; i++) {
        cout << "\nCourse " << i+1 << " ka naam/code: ";
        cin >> course[i];

        cout << "Credit Hours: ";
        cin >> credit[i];

        cout << "Grade A/B/C/D/F: ";
        cin >> grade[i];

        double gp = gradeToPoint(grade[i]);
        if(gp == -1) {
            cout << "Galat grade! A/B/C/D/F daalo. Phir se try karo.\n";
            i--; // same course dobara
            continue;
        }

        totalGradePoints += gp * credit[i];
        totalCredit += credit[i];
    }

    double semesterGPA = totalGradePoints / totalCredit;

    // Output display - CodeAlpha ka requirement
    cout << "\n=====================================";
    cout << "\n--- Semester Result ---\n";
    cout << "Course\tCredit\tGrade\tGrade Points\n";
    cout << "-------------------------------------" << endl;

    for(int i=0; i<n; i++) {
        double gp = gradeToPoint(grade[i]) * credit[i];
        cout << course[i] << "\t\t" << credit[i] << "\t" << grade[i] << "\t" << gp << endl;
    }

    cout << "-------------------------------------" << endl;
    cout << fixed << setprecision(2); // 2 decimal tak
    cout << "Total Credit Hours: " << totalCredit << endl;
    cout << "Total Grade Points: " << totalGradePoints << endl;
    cout << "Semester GPA: " << semesterGPA << endl;
    cout << "Overall CGPA: " << semesterGPA << " <-- Current semester" << endl;
    cout << "=====================================" << endl;

    cout << "\nNote: CGPA = purane semesters + current semester / total semesters";
    cout << "\nAgar ye 1st semester hai to CGPA = GPA hi hoga ✅\n";

    return 0;
}
