# Assignment 7


## Problem Statement
WAP to implement Bubble sort and Quick Sort on a 1D array of Student structure (contains student_name, student_roll_no, total_marks), with key as student_roll_no. And count the number of swap performed by each method.

## Theory
Sorting is a common operation in data structures.  
- **Bubble Sort** repeatedly swaps adjacent elements if they are in the wrong order.  
- **Quick Sort** uses a pivot to partition the array and recursively sort subarrays.  
Tracking swaps helps understand the algorithm’s behavior.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

typedef struct 
{
    char name_psk[50];
    int rollNo_psk;
    float marks_psk;
} Student;

void PrintingRolls(Student* arr, int n_psk)
{
    for(int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        cout << arr[i_psk].rollNo_psk << " ";  
    }
    cout << "\n";
}

void BubbleSort(Student* arr, int n_psk)
{
    int swaps_psk = 0;
    Student temp;
    int swapped_psk;

    for(int i_psk = 0; i_psk < n_psk - 1; i_psk++)
    {
        swapped_psk = 0;
        cout << "\nPass " << i_psk + 1 << ": \n";
        for(int j_psk = 0; j_psk < n_psk - i_psk - 1; j_psk++)
        {
            if(arr[j_psk].rollNo_psk > arr[j_psk+1].rollNo_psk)
            {
                cout << "Swapping " << arr[j_psk].rollNo_psk << " with " << arr[j_psk+1].rollNo_psk << "\n";
                temp = arr[j_psk];
                arr[j_psk] = arr[j_psk+1];
                arr[j_psk+1] = temp;
                swaps_psk++;
                swapped_psk = 1;
                cout << "After swapping: ";
                PrintingRolls(arr, n_psk);
            }
        }

        if(!swapped_psk)
        {
            cout << "No need to swap. Array is sorted.\n";
            break;
        }
    }

    cout << "\nTotal swaps performed: " << swaps_psk << "\n";
}

int quickSwaps_psk = 0;

int partition(Student* arr, int first_psk, int last_psk, int n_psk)
{
    int pivot_psk = arr[first_psk].rollNo_psk;
    int count_psk = 0;

    for(int i_psk = first_psk + 1; i_psk <= last_psk; i_psk++)
    {
        if(arr[i_psk].rollNo_psk < pivot_psk)
        {
            count_psk++;
        }
    }

    int pivotIndex_psk = first_psk + count_psk;

    cout << "Swapping " << arr[first_psk].rollNo_psk << " with " << arr[pivotIndex_psk].rollNo_psk << "\n";
    Student temp = arr[pivotIndex_psk];
    arr[pivotIndex_psk] = arr[first_psk];
    arr[first_psk] = temp;
    quickSwaps_psk++;
    cout << "After swapping: ";
    PrintingRolls(arr, n_psk);

    int i_psk = first_psk;
    int j_psk = last_psk;

    while(i_psk < pivotIndex_psk && j_psk > pivotIndex_psk)
    {
        while(arr[i_psk].rollNo_psk < arr[pivotIndex_psk].rollNo_psk)
        {
            i_psk++;
        }
        while(arr[j_psk].rollNo_psk > arr[pivotIndex_psk].rollNo_psk)
        {
            j_psk--;
        }

        if(i_psk < pivotIndex_psk && j_psk > pivotIndex_psk)
        {
            cout << "Swapping " << arr[i_psk].rollNo_psk << " with " << arr[j_psk].rollNo_psk << "\n";
            temp = arr[i_psk];
            arr[i_psk] = arr[j_psk];
            arr[j_psk] = temp;
            cout << "After swapping: ";
            PrintingRolls(arr, n_psk);
            
            i_psk++;
            j_psk--;
        }
    }

    return(pivotIndex_psk);
}

void QuickSort(Student* arr, int first_psk, int last_psk, int n_psk)
{
    if(first_psk >= last_psk)
    {
        return;
    }

    int p_psk = partition(arr, first_psk, last_psk, n_psk);

    QuickSort(arr, first_psk, p_psk - 1, n_psk);
    QuickSort(arr, p_psk + 1, last_psk, n_psk);
}

int main(void)
{
    int n_psk = 8;

    Student temp[] = {
        {"Ravi", 23, 78.5f},
        {"Sneha", 12, 82.0f},
        {"Amit", 35, 91.2f},
        {"Priya", 18, 69.0f},
        {"Karan", 7, 88.5f},
        {"Meera", 29, 76.0f},
        {"Anjali", 15, 84.3f},
        {"Rahul", 31, 90.0f}
    };

    Student* students = new Student[n_psk];

    for(int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        students[i_psk] = temp[i_psk];
    }

    cout << "Initial RollNos: ";
    PrintingRolls(students, n_psk);

    BubbleSort(students, n_psk);

    cout << "\nAfter sorting: \n";
    for(int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        cout << students[i_psk].name_psk << "   RollNo: " << students[i_psk].rollNo_psk << "   Marks: " << students[i_psk].marks_psk << "\n";
    }

    for(int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        students[i_psk] = temp[i_psk];
    }

    quickSwaps_psk = 0;

    cout << "\nInitial RollNos: ";
    PrintingRolls(students, n_psk);

    cout << "\n-----Quick Sort-----\n";

    QuickSort(students,0, n_psk - 1, n_psk);

    cout << "\nAfter sorting: \n";
    for(int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        cout << students[i_psk].name_psk << "   RollNo: " << students[i_psk].rollNo_psk << "   Marks: " << students[i_psk].marks_psk << "\n";
    }

    cout << "\nTotal swaps performed in Quick Sort: " << quickSwaps_psk << "\n";

    delete[] students;

    return 0;
}

```

## Output
![Program Output](Assignment7(Output1).png)
![Program Output](Assignment7(Output2).png)