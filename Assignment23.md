# Assignment 23


## Problem Statement
Write a program to implement multiple stack i.e more than two stack using array and perform following operations on it. A. Push B. Pop C. Stack Overflow D. Stack Underflow E. Display

## Theory
A multiple-stack structure allows storing more than two stacks within one array. This is used when memory must be shared efficiently across several LIFO structures. A single array can be divided into fixed sections for each stack (static partitioning), or dynamic partitioning can be used to allow flexible growth.
Operations like push and pop must verify the boundaries of their respective partitions to prevent overflow and underflow. Implementing multiple stacks reduces memory waste, especially in environments where several stack-based operations occur simultaneously, such as in recursion engines or multiple expression evaluators. It also demonstrates important concepts related to memory management, indexing, and boundary checking.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

#define MAX 30
#define NUM_STACK 3

int arr[MAX];
int top[NUM_STACK];
int stackSize;

void initialize()
{
    stackSize = MAX / NUM_STACK;
    for(int i = 0; i < NUM_STACK; i++)
    {
        top[i] = -1;
    }
}

void push(int stackNumber, int value)
{
    int idx = stackNumber - 1;
    if(top[idx] >= stackSize - 1)
    {
        cout<<"Stack "<<stackNumber<<" Overflow!";
        return;
    }

    top[idx]++;
    arr[idx * stackSize + top[idx]] = value;
    cout<<value<<" pushed to stack "<<stackNumber<<endl;
}

void pop(int stackNumber)
{
    int idx = stackNumber - 1;
    if(top[idx] == -1)
    {
        cout<<"Stack "<<stackNumber<<" Underflow!\n";
        return;
    }

    int value = arr[idx * stackSize + top[idx]];
    top[idx]--;
    cout<<value<<" popped from stack "<<stackNumber<<endl;
}

void displayStack(int stackNumber)
{
    int idx = stackNumber - 1;
    if(top[idx] == -1)
    {
        cout<<"Stack "<<stackNumber<<" Underflow!\n";
        return;
    }

    cout<<"Stack "<<stackNumber<<": ";
    for(int i = 0; i <=top[idx]; i++)
    {
        cout<<arr[idx * stackSize + i]<<" ";
    }
    cout<<endl;
}

int main()
{
    initialize();
    int ch, stackNum, val;

    while(true)
    {
        cout<<"\n-----Multiple Stack-----\n";
        cout<<"1. Push\n2. Pop\n3. Display\n4. Exit\n";
        cout<<"Enter your choice: ";
        cin>>ch;

        switch(ch)
        {
            case 1:
                cout<<"Enter stack number: ";
                cin>>stackNum;
                cout<<"Enter value: ";
                cin>>val;
                push(stackNum, val);
                break;

            case 2:
                cout<<"Enter stack number: ";
                cin>>stackNum;
                pop(stackNum);
                break;

            case 3:
                cout<<"Enter stack number: ";
                cin>>stackNum;
                displayStack(stackNum);
                break;

            case 4:
                cout<<"Exiting...";
                exit(0);

            default:
                cout<<"Invalid choice!\n";
        }
    }
    return 0;
}

```

## Output
-----Multiple Stack-----
1. Push
2. Pop
3. Display
4. Exit
Enter your choice: 1
Enter stack number: 1
Enter value: 20
20 pushed to stack 1

-----Multiple Stack-----
1. Push
2. Pop
3. Display
4. Exit
Enter your choice: 1
Enter stack number: 1
Enter value: 40
40 pushed to stack 1

-----Multiple Stack-----
1. Push
2. Pop
3. Display
4. Exit
Enter your choice: 1
Enter stack number: 2
Enter value: 50
50 pushed to stack 2

-----Multiple Stack-----
1. Push
2. Pop
3. Display
4. Exit
Enter your choice: 1
Enter stack number: 2
Enter value: 60
60 pushed to stack 2

-----Multiple Stack-----
1. Push
2. Pop
3. Display
4. Exit
Enter your choice: 3
Enter stack number: 1
Stack 1: 20 40

-----Multiple Stack-----
1. Push
2. Pop
3. Display
4. Exit
Enter your choice: 3
Enter stack number: 2
Stack 2: 50 60

## Real-Life Applications
•	Virtual machines that maintain multiple stacks for registers, calls, and operands
•	Browser engines that maintain stacks for parsing scripts, styles, and DOM events
•	Simultaneous expression evaluators
•	Real-time operating systems managing multiple task stacks
•	Memory-constrained embedded systems

## Conclusion
Multiple stacks in a single array demonstrate efficient memory utilization and controlled handling of several LIFO structures at once. This approach is vital for systems requiring parallel stack operations with minimal memory overhead.