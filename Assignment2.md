# Assignment 2

## Problem Statement
Write a program to construct and verify a magic square of order 'n' (for both even & odd) such that all rows, columns, and diagonals sum to the same value.

## Theory
A **magic square** is an `n x n` matrix of distinct integers from 1 to n² such that the sum of numbers in each row, each column, and both main diagonals is the same.  

This program demonstrates:
- Dynamic memory allocation for 2D arrays.  
- Handling **odd-order** magic squares using the Siamese method.  
- Handling **doubly-even order** magic squares using the specific pattern method.  
- Manual iteration and logic without using built-in matrix libraries. 

## Code
```cpp
#include <iostream>
using namespace std;

int main()
{
    int n_psk;
    cout << "Enter the value of n: ";
    cin >> n_psk;

    if (n_psk <= 0)
    {
        cout << "Error: n must be a positive integer!" << endl;
        return -1;
    }

    int** magic_square_psk = new int*[n_psk];
    for (int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        magic_square_psk[i_psk] = new int[n_psk];
        for (int j_psk = 0; j_psk < n_psk; j_psk++)
        {
            magic_square_psk[i_psk][j_psk] = 0;
        }
    }

    if (n_psk % 2 == 1) 
    {
        int row_psk = 0;
        int col_psk = n_psk / 2;

        for (int num_psk = 1; num_psk <= n_psk * n_psk; num_psk++)
        {
            magic_square_psk[row_psk][col_psk] = num_psk;

            int next_row_psk = row_psk - 1;
            int next_col_psk = col_psk + 1;

            if (next_row_psk < 0) 
                next_row_psk = n_psk - 1;
            if (next_col_psk == n_psk) 
                next_col_psk = 0;

            if (magic_square_psk[next_row_psk][next_col_psk] != 0)
            {
                next_row_psk = (row_psk + 1) % n_psk;
                next_col_psk = col_psk;
            }

            row_psk = next_row_psk;
            col_psk = next_col_psk;
        }
    }
    else if (n_psk % 4 == 0) 
    {
        int num_psk = 1;
        int n2_psk = n_psk * n_psk;

        for (int i_psk = 0; i_psk < n_psk; i_psk++)
        {
            for (int j_psk = 0; j_psk < n_psk; j_psk++)
            {
                if (((i_psk % 4 == j_psk % 4) || ((i_psk % 4 + j_psk % 4) == 3)))
                {
                    magic_square_psk[i_psk][j_psk] = num_psk;
                }
                else
                {
                    magic_square_psk[i_psk][j_psk] = n2_psk - num_psk + 1;
                }
                num_psk++;
            }
        }
    }

    for (int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        for (int j_psk = 0; j_psk < n_psk; j_psk++)
        {
            cout << magic_square_psk[i_psk][j_psk] << "\t";
        }
        cout << endl;
    }

    cout << "Magic sum: " << n_psk * (n_psk * n_psk + 1) / 2 << endl;

    for (int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        delete[] magic_square_psk[i_psk];
    }
    delete[] magic_square_psk;

    return 0;
}
```

## Output
![Program Output](Assignment2(Output).png)
