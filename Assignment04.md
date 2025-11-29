# Assignment 4

## Problem Statement
Develop a program to identify and efficiently store a sparse matrix using compact representation and perform basic operations like display and simple transpose.

## Theory
A **sparse matrix** is a matrix in which most of the elements are zero.  
Storing all elements is memory-inefficient, so we store only **non-zero elements** in a triplet format:
Transposing a sparse matrix involves switching the **row and column indices** for each non-zero element while preserving the triplet structure.  
This program demonstrates:
- Dynamic allocation for 2D arrays.
- Counting non-zero elements.
- Creating triplet representation.
- Computing transpose manually.

## Code
```cpp
#include <iostream>
using namespace std;

int main(void)
{
    int n_rows1_psk, n_cols1_psk;

    cout << "\n Enter number of rows: ";
    cin >> n_rows1_psk;
    cout << "\n Enter number of columns: ";
    cin >> n_cols1_psk;

    int** matrix_psk = new int*[n_rows1_psk];
    for (int i_psk = 0; i_psk < n_rows1_psk; i_psk++) {
        matrix_psk[i_psk] = new int[n_cols1_psk];
    }

    for (int i_psk = 0; i_psk < n_rows1_psk; i_psk++) {
        for (int j_psk = 0; j_psk < n_cols1_psk; j_psk++) {
            cout << "Enter element [" << i_psk << "][" << j_psk << "]: ";
            cin >> matrix_psk[i_psk][j_psk];
        }
    }

    int nonZero_psk = 0;
    for (int i_psk = 0; i_psk < n_rows1_psk; i_psk++) {
        for (int j_psk = 0; j_psk < n_cols1_psk; j_psk++) {
            if (matrix_psk[i_psk][j_psk] != 0)
                nonZero_psk++;
        }
    }

    int** sparse_psk = new int*[nonZero_psk + 1];
    for (int i_psk = 0; i_psk <= nonZero_psk; i_psk++) {
        sparse_psk[i_psk] = new int[3];
    }

    int k_psk = 1;
    for (int i_psk = 0; i_psk < n_rows1_psk; i_psk++) {
        for (int j_psk = 0; j_psk < n_cols1_psk; j_psk++) {
            if (matrix_psk[i_psk][j_psk] != 0) {
                sparse_psk[k_psk][0] = i_psk;
                sparse_psk[k_psk][1] = j_psk;
                sparse_psk[k_psk][2] = matrix_psk[i_psk][j_psk];
                k_psk++;
            }
        }
    }

    sparse_psk[0][0] = n_rows1_psk;
    sparse_psk[0][1] = n_cols1_psk;
    sparse_psk[0][2] = nonZero_psk;

    cout << "\n\tRows Columns Values:";
    for (int i_psk = 0; i_psk <= sparse_psk[0][2]; i_psk++) {
        cout << "\n";
        for (int j_psk = 0; j_psk < 3; j_psk++) {
            cout << "\t" << sparse_psk[i_psk][j_psk];
        }
    }

    int** transpose_psk = new int*[nonZero_psk + 1];
    for (int i_psk = 0; i_psk <= nonZero_psk; i_psk++) {
        transpose_psk[i_psk] = new int[3];
    }

    int k2_psk = 1;
    for (int z_psk = 0; z_psk < sparse_psk[0][1]; z_psk++) {
        for (int i_psk = 1; i_psk <= sparse_psk[0][2]; i_psk++) {
            if (sparse_psk[i_psk][1] == z_psk) {
                transpose_psk[k2_psk][0] = sparse_psk[i_psk][1];
                transpose_psk[k2_psk][1] = sparse_psk[i_psk][0];
                transpose_psk[k2_psk][2] = sparse_psk[i_psk][2];
                k2_psk++;
            }
        }
    }

    transpose_psk[0][0] = sparse_psk[0][1];
    transpose_psk[0][1] = sparse_psk[0][0];
    transpose_psk[0][2] = sparse_psk[0][2];

    cout << "\n\tTranspose Triplet:";
    for (int i_psk = 0; i_psk <= transpose_psk[0][2]; i_psk++) {
        cout << "\n";
        for (int j_psk = 0; j_psk < 3; j_psk++) {
            cout << "\t" << transpose_psk[i_psk][j_psk];
        }
    }

    for (int i_psk = 0; i_psk < n_rows1_psk; i_psk++){
        delete[] matrix_psk[i_psk];
    }
    delete[] matrix_psk;

    for (int i_psk = 0; i_psk <= nonZero_psk; i_psk++){
        delete[] sparse_psk[i_psk];
    }
    delete[] sparse_psk;

    for (int i_psk = 0; i_psk <= nonZero_psk; i_psk++){ 
        delete[] transpose_psk[i_psk];
    }
    delete[] transpose_psk;

    return 0;
}

```

## Output
![Program Output](Assignment4(Output).png)