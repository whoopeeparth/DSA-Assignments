# Assignment 5


## Problem Statement
Develop a program to compute the fast transpose of a sparse matrix using its compact (triplet) representation efficiently.

## Theory
A sparse matrix has most elements as zero. Instead of storing all elements, we store only the **non-zero elements** in triplet form `[row, column, value]`.  
The **fast transpose** method efficiently transposes a sparse matrix by directly placing each element in its correct position.

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
    for (int i_psk = 0; i_psk < nonZero_psk + 1; i_psk++) {
        sparse_psk[i_psk] = new int[3];
    }

    sparse_psk[0][0] = n_rows1_psk;
    sparse_psk[0][1] = n_cols1_psk;
    sparse_psk[0][2] = nonZero_psk;

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

    cout << "\n\tRows Columns Values: ";
    for (int i_psk = 0; i_psk <= sparse_psk[0][2]; i_psk++) {
        cout << "\n";
        for (int j_psk = 0; j_psk < 3; j_psk++) {
            cout << "\t" << sparse_psk[i_psk][j_psk];
        }
    }

    int* total_psk = new int[sparse_psk[0][1]]();         
    int* index_psk = new int[sparse_psk[0][1] + 1]();         

    for (int i_psk = 1; i_psk <= sparse_psk[0][2]; i_psk++) {
        int col_no_psk = sparse_psk[i_psk][1];
        total_psk[col_no_psk]++;
    }

    index_psk[0] = 1;
    for (int i_psk = 1; i_psk <= sparse_psk[0][1]; i_psk++) {
        index_psk[i_psk] = index_psk[i_psk - 1] + total_psk[i_psk - 1];
    }

    int** result_psk = new int*[nonZero_psk + 1];
    for (int i_psk = 0; i_psk < nonZero_psk + 1; i_psk++) {
        result_psk[i_psk] = new int[3];
    }

    result_psk[0][0] = sparse_psk[0][1];  
    result_psk[0][1] = sparse_psk[0][0];
    result_psk[0][2] = sparse_psk[0][2];

    for (int i_psk = 1; i_psk <= sparse_psk[0][2]; i_psk++) {
        int col_no_psk = sparse_psk[i_psk][1];
        int loc_psk = index_psk[col_no_psk];
        result_psk[loc_psk][0] = sparse_psk[i_psk][1];
        result_psk[loc_psk][1] = sparse_psk[i_psk][0];
        result_psk[loc_psk][2] = sparse_psk[i_psk][2];
        index_psk[col_no_psk]++;
    }

    cout << "\n\n\tFast Transpose:";
    for (int i_psk = 0; i_psk <= result_psk[0][2]; i_psk++) {
        cout << "\n";
        for (int j_psk = 0; j_psk < 3; j_psk++) {
            cout << "\t" << result_psk[i_psk][j_psk];
        }
    }

    for (int i_psk = 0; i_psk < n_rows1_psk; i_psk++) {
        delete[] matrix_psk[i_psk];
    }
    delete[] matrix_psk;

    for (int i_psk = 0; i_psk < nonZero_psk + 1; i_psk++) {
        delete[] sparse_psk[i_psk];
    }
    delete[] sparse_psk;

    for (int i_psk = 0; i_psk < nonZero_psk + 1; i_psk++) {
        delete[] result_psk[i_psk];
    }
    delete[] result_psk;

    delete[] total_psk;
    delete[] index_psk;

    return 0;
}

```

## Output
![Program Output](Assignment5(Output).png)