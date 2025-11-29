# Assignment 9


## Problem Statement
Write a program using Bubble sort algorithm, assign the roll nos. to the students of your class as per their previous years result. i.e. topper will be roll no. 1 and analyse the sorting algorithm pass by pass.

## Theory
Bubble Sort repeatedly swaps adjacent elements to sort the array.  
Here, it is applied to **student marks**, and roll numbers are updated to reflect the ranking.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

typedef struct 
{
    char name_psk[50];
    int marks_psk;
    int rollNo_psk;
} Student;

void SortByMarks(Student* students, int n_psk)
{
    Student temp;
    int i_psk, j_psk, swapped_psk;
    for(i_psk = 0; i_psk < n_psk - 1; i_psk++)
    {
        swapped_psk = 0;
        cout << "\nPass " << i_psk + 1 << ": \n";
        for(j_psk = 0; j_psk < n_psk - i_psk - 1; j_psk++)
        {
            if(students[j_psk].marks_psk < students[j_psk+1].marks_psk)
            {
                cout << "Swapping " << students[j_psk].marks_psk << " with " << students[j_psk+1].marks_psk << "\n";
                temp = students[j_psk];
                students[j_psk] = students[j_psk+1];
                students[j_psk+1] = temp;

                swapped_psk = 1;

                cout << "After swapping: \n";
                for(int k_psk = 0; k_psk < n_psk; k_psk++)
                {
                    cout << students[k_psk].marks_psk << " ";
                }

                cout << "\n";
            }
        }

        if(!swapped_psk)
        {
            cout << "Array has been sorted.\n";
            break;
        }
    }

    for(i_psk = 0; i_psk < n_psk; i_psk++)
    {
        students[i_psk].rollNo_psk = i_psk + 1; 
    }
}

int main(void)
{
    int n_psk = 10;

    Student temp[] = {
        {"Alice", 85, 0},
        {"Bob", 92, 0},
        {"Charlie", 78, 0},
        {"David", 90, 0},
        {"Eve", 88, 0},
        {"Frank", 75, 0},
        {"Grace", 95, 0},
        {"Hannah", 80, 0},
        {"Ian", 82, 0},
        {"Jack", 89, 0}
    };

    Student* students = new Student[n_psk];

    if(students == NULL)
    {
        cout << "Memory allocation failed.\n";
        exit(-1);
    }

    for(int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        students[i_psk] = temp[i_psk];
    }

    cout << "Original array: \n";
    for(int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        cout << students[i_psk].name_psk << " : " << students[i_psk].marks_psk << "\n";
    }
    cout << "\n";

    SortByMarks(students, n_psk);

    cout << "\nFinal sorted array: \n";
    for(int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        cout << "RollNo " << students[i_psk].rollNo_psk << ": " << students[i_psk].name_psk << " Marks: " << students[i_psk].marks_psk << "\n";
    }

    delete[] students;

    return 0;
}

```

## Output
![Program Output](Assignment9(Output1).png)
![Program Output](Assignment9(Output2).png)