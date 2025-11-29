# Assignment 8


## Problem Statement
Write a program to input marks of n students Sort the marks in ascending order using the Quick Sort algorithm without using built-in library functions and analyse the sorting algorithm pass by pass. Find the minimum and maximum marks using Divide and Conquer (recursively).

## Theory
Quick Sort is an efficient divide-and-conquer sorting algorithm.  
Finding minimum and maximum marks recursively allows **O(n) comparisons** in a structured manner.

## Code
```cpp
#include <iostream>
#include <cstdlib>  
using namespace std;

int quickSwaps_psk = 0;
int passCount_psk = 0;

void PrintArray(int arr_psk[], int n_psk)
{
    for (int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        cout << arr_psk[i_psk] << " ";
    }
    cout << endl;
}

int partition(int arr_psk[], int first_psk, int last_psk, int n_psk)
{
    int pivot_psk = arr_psk[first_psk];
    int count_psk = 0;

    for (int i_psk = first_psk + 1; i_psk <= last_psk; i_psk++)
    {
        if (arr_psk[i_psk] < pivot_psk)
        {
            count_psk++;
        }
    }

    int pivotIndex_psk = first_psk + count_psk;
    cout << "Swapping " << arr_psk[first_psk] << " with " << arr_psk[pivotIndex_psk] << endl;

    int temp_psk = arr_psk[pivotIndex_psk];
    arr_psk[pivotIndex_psk] = arr_psk[first_psk];
    arr_psk[first_psk] = temp_psk;
    quickSwaps_psk++;

    cout << "After swapping: ";
    PrintArray(arr_psk, n_psk);

    int i_psk = first_psk;
    int j_psk = last_psk;

    while (i_psk < pivotIndex_psk && j_psk > pivotIndex_psk)
    {
        while (arr_psk[i_psk] < arr_psk[pivotIndex_psk])
        {
            i_psk++;
        }
        while (arr_psk[j_psk] > arr_psk[pivotIndex_psk])
        {
            j_psk--;
        }
        if (i_psk < pivotIndex_psk && j_psk > pivotIndex_psk)
        {
            cout << "Swapping " << arr_psk[i_psk] << " with " << arr_psk[j_psk] << endl;
            temp_psk = arr_psk[i_psk];
            arr_psk[i_psk] = arr_psk[j_psk];
            arr_psk[j_psk] = temp_psk;
            quickSwaps_psk++;

            cout << "After swapping: ";
            PrintArray(arr_psk, n_psk);

            i_psk++;
            j_psk--;
        }
    }

    return pivotIndex_psk;
}

void QuickSort(int arr_psk[], int first_psk, int last_psk, int n_psk)
{
    if (first_psk >= last_psk)
        return;

    passCount_psk++;
    cout << "\nPass " << passCount_psk << ":\n";

    int p_psk = partition(arr_psk, first_psk, last_psk, n_psk);

    QuickSort(arr_psk, first_psk, p_psk - 1, n_psk);
    QuickSort(arr_psk, p_psk + 1, last_psk, n_psk);
}

void FindMinMax(int arr_psk[], int first_psk, int last_psk, int* min_psk, int* max_psk)
{
    if (first_psk == last_psk)
    {
        *min_psk = arr_psk[first_psk];
        *max_psk = arr_psk[first_psk];
        return;
    }

    int mid_psk = (first_psk + last_psk) / 2;
    int min1_psk, max1_psk, min2_psk, max2_psk;

    FindMinMax(arr_psk, first_psk, mid_psk, &min1_psk, &max1_psk);
    FindMinMax(arr_psk, mid_psk + 1, last_psk, &min2_psk, &max2_psk);

    if(min1_psk < min2_psk)
    {
        *min_psk = min1_psk;
    }
    else
    {
        *min_psk = min2_psk;
    }

    if(max1_psk > max2_psk)
    {
        *max_psk = max1_psk;
    }
    else
    {
        *max_psk = max2_psk;
    }
}

int main()
{
    int n_psk;
    cout << "Enter number of students: ";
    cin >> n_psk;

    int* marks_psk = new int[n_psk];

    for (int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        marks_psk[i_psk] = rand() % 100;
    }

    cout << "\nInitial Marks: ";
    PrintArray(marks_psk, n_psk);

    QuickSort(marks_psk, 0, n_psk - 1, n_psk);

    cout << "\nSorted Marks: ";
    PrintArray(marks_psk, n_psk);

    cout << "Total swaps performed: " << quickSwaps_psk << endl;

    int min_psk, max_psk;
    FindMinMax(marks_psk, 0, n_psk - 1, &min_psk, &max_psk);

    cout << "\nMinimum marks: " << min_psk << endl;
    cout << "Maximum marks: " << max_psk << endl;

    delete[] marks_psk;

    return 0;
}

```

## Output
![Program Output](Assignment8(Output).png)