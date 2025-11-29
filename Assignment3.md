# Assignment 3

## Problem Statement
Implement matrix multiplication and analyse its performance using row-major vs column-major order access patterns to understand how memory layout affects cache performance.	

## Theory
Matrix multiplication is a fundamental operation in computer science and numerical computing.  
This program demonstrates:
- Dynamic memory allocation for 2D arrays.
- Row-major vs Column-major multiplication order.
- Performance measurement using `clock()` function.
- Random initialization of matrices for testing.
- Proper memory deallocation. 

## Code
```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main()
{
    int n_psk = 500;

    int** A = new int*[n_psk];
    int** B = new int*[n_psk];
    int** C = new int*[n_psk];

    for (int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        A[i_psk] = new int[n_psk];
        B[i_psk] = new int[n_psk];
        C[i_psk] = new int[n_psk];
    }

    cout << "Assign random values to matrices:\n";
    srand(time(0));
    for (int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        for (int j_psk = 0; j_psk < n_psk; j_psk++)
        {
            A[i_psk][j_psk] = rand() % 10;
            B[i_psk][j_psk] = rand() % 10;
            C[i_psk][j_psk] = 0;
        }
    }

    if (n_psk <= 5)
    {
        cout << "\nInitial A matrix:\n";
        for (int i_psk = 0; i_psk < n_psk; i_psk++)
        {
            for (int j_psk = 0; j_psk < n_psk; j_psk++)
            {
                cout << A[i_psk][j_psk] << " ";
            }
            cout << endl;
        }

        cout << "Initial B matrix:\n";
        for (int i_psk = 0; i_psk < n_psk; i_psk++)
        {
            for (int j_psk = 0; j_psk < n_psk; j_psk++)
            {
                cout << B[i_psk][j_psk] << " ";
            }
            cout << endl;
        }
    }

    clock_t start, end;
    double time_used;

    start = clock();
    for (int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        for (int k_psk = 0; k_psk < n_psk; k_psk++)
        {
            for (int j_psk = 0; j_psk < n_psk; j_psk++)
            {
                C[i_psk][j_psk] += A[i_psk][k_psk] * B[k_psk][j_psk];
            }
        }
    }
    end = clock();
    time_used = double(end - start) / CLOCKS_PER_SEC;

    if (n_psk <= 5)
    {
        cout << "\nResult Row Major Matrix:\n";
        for (int i_psk = 0; i_psk < n_psk; i_psk++)
        {
            for (int j_psk = 0; j_psk < n_psk; j_psk++)
            {
                cout << C[i_psk][j_psk] << " ";
            }
            cout << endl;
        }
    }
    cout << "Row Major Time: " << time_used << " seconds\n";

    for (int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        for (int j_psk = 0; j_psk < n_psk; j_psk++)
        {
            C[i_psk][j_psk] = 0;
        }
    }

    start = clock();
    for (int j_psk = 0; j_psk < n_psk; j_psk++)
    {
        for (int k_psk = 0; k_psk < n_psk; k_psk++)
        {
            for (int i_psk = 0; i_psk < n_psk; i_psk++)
            {
                C[i_psk][j_psk] += A[i_psk][k_psk] * B[k_psk][j_psk];
            }
        }
    }
    end = clock();
    time_used = double(end - start) / CLOCKS_PER_SEC;

    if (n_psk <= 5)
    {
        cout << "\nResult Column Major Matrix:\n";
        for (int i_psk = 0; i_psk < n_psk; i_psk++)
        {
            for (int j_psk = 0; j_psk < n_psk; j_psk++)
            {
                cout << C[i_psk][j_psk] << " ";
            }
            cout << endl;
        }
    }
    cout << "Column Major Time: " << time_used << " seconds\n";

    for (int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        delete[] A[i_psk];
        delete[] B[i_psk];
        delete[] C[i_psk];
    }
    delete[] A;
    delete[] B;
    delete[] C;

    return 0;
}

```

## Output
![Program Output](Assignment3(Output).png)
