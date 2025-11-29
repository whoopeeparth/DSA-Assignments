# Assignment 10


## Problem Statement
Write a program to arrange the list of employees as per the average of their height and weight by using Merge and Selection sorting method. Analyse their time complexities and conclude which algorithm will take less time to sort the list. 

## Theory
Merge Sort is a **divide-and-conquer algorithm** that splits the array into halves, sorts them recursively, and merges.  
Selection Sort repeatedly selects the **minimum element** and swaps it to the correct position.  
This program compares both sorting methods on randomly generated employee averages.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

void MergeSort(float*, int, int);
void Merge(float*, int, int, int);
void SelectionSort(float*, int);
void PrintArray(float*, int);

int main(void)
{
    int n_psk;
    cout << "Enter number of employees: ";
    cin >> n_psk;

    float *avg = new float[n_psk];
    float *original = new float[n_psk];
    float height_psk, weight_psk;

    if(avg == nullptr || original == nullptr)
    {
        cout << "Memory allocation failed.\n";
        exit(-1);
    }

    cout << "Random generated inputs: \n";
    for(int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        height_psk = (rand() % 51) + 150;
        weight_psk = (rand() % 51) + 50;
        avg[i_psk] = (weight_psk + height_psk) / 2.0;
        original[i_psk] = avg[i_psk];

        cout << "Employee " << i_psk + 1 << ": Height: " << height_psk << ", Weight: " << weight_psk << ", Average: " << avg[i_psk] << "\n";
    }

    cout << "\n Original Averages: ";
    PrintArray(avg, n_psk);

    cout << "\n-----Merge Sort-----\n";
    MergeSort(avg, 0, n_psk - 1);
    cout << "\nSorted averages: ";
    PrintArray(avg, n_psk);

    for(int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        avg[i_psk] = original[i_psk];
    }

    cout << "\n-----Selection Sort-----\n";
    SelectionSort(avg, n_psk);
    cout << "\nSorted Averages: ";
    PrintArray(avg, n_psk);

    delete[] avg;
    avg = nullptr;
    delete[] original;
    original = nullptr;

    return 0;

}

void PrintArray(float* arr, int n_psk)
{
    for(int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        cout << arr[i_psk] << " ";
    }
    cout << "\n";
}

void SelectionSort(float* arr, int n_psk)
{
    int i_psk, j_psk, minIndex_psk;
    float temp_psk;

    for (i_psk = 0; i_psk < n_psk - 1; i_psk++)
    {
        minIndex_psk = i_psk;

        for (j_psk = i_psk + 1; j_psk < n_psk; j_psk++)
        {
            if (arr[j_psk] < arr[minIndex_psk])
            {
                minIndex_psk = j_psk;
            }
        }

        cout << "\nPASS " << i_psk + 1 << ":\n";

        if (minIndex_psk != i_psk)
        {
            cout << "Swapping " << arr[i_psk] << " with " << arr[minIndex_psk] << "\n";
            temp_psk = arr[i_psk];
            arr[i_psk] = arr[minIndex_psk];
            arr[minIndex_psk] = temp_psk;
        }
        else
        {
            cout << "Nothing to swap\n";
        }

        cout << "Array after PASS " << i_psk + 1 << ": ";
        PrintArray(arr, n_psk);
    }
}

void Merge(float* arr, int first_psk, int mid_psk, int last_psk)
{
    int len1_psk = mid_psk - first_psk + 1;
    int len2_psk = last_psk - mid_psk;

    float* L = new float[len1_psk];
    float* R = new float[len2_psk];

    if(L == nullptr || R == nullptr)
    {
        cout << "Memory allocation failed.\n";
        exit(-2);
    }

    int i_psk, j_psk, k_psk;

    k_psk = first_psk;
    for(i_psk = 0; i_psk < len1_psk; i_psk++)
    {
        L[i_psk] = arr[k_psk];
        k_psk++;
    }

    k_psk = mid_psk + 1;
    for(j_psk = 0; j_psk < len2_psk; j_psk++)
    {
        R[j_psk] = arr[k_psk];
        k_psk++;
    }

    i_psk = 0;
    j_psk = 0;
    k_psk = first_psk;

    while(i_psk < len1_psk && j_psk < len2_psk)
    {
        if(L[i_psk] < R[j_psk])
        {
            arr[k_psk] = L[i_psk];
            k_psk++;
            i_psk++;
        }
        else
        {
            arr[k_psk] = R[j_psk];
            k_psk++;
            j_psk++;
        }
    }

    while(i_psk < len1_psk)
    {
        arr[k_psk] = L[i_psk];
        k_psk++;
        i_psk++;
    }

    while(j_psk < len2_psk)
    {
        arr[k_psk] = R[j_psk];
        k_psk++;
        j_psk++;
    }

    delete[] L;
    L = nullptr;
    delete[] R;
    R = nullptr;
}

void MergeSort(float* arr, int first_psk, int last_psk)
{
    if(first_psk < last_psk)
    {
        int mid_psk = (first_psk + last_psk) / 2;
        MergeSort(arr, first_psk, mid_psk);
        MergeSort(arr, mid_psk + 1, last_psk);
        Merge(arr, first_psk, mid_psk, last_psk);
    }
}

```

## Output
![Program Output](Assignment10(Output).png)