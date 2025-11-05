# Student-Record-management-system-by-using-linked-list
Name : Anisha Pravin

Roll no : 1/24/SET/BCS/093

Section : 3CSB

subject : DSA

Faculty member : Dr Lenin Narengban

Department : Computer Science Engineering and Technology


#Description( Student-Record-management-system-by-using-linked-list)

The Student Record Management System using Linked List is a simple console-based application written in C. It manages student data such as roll number, name, age, and marks. Each student record is stored as a node in a linked list.
A linked list is used because it allows dynamic memory allocation, meaning new records can be added or removed easily during runtime. Each node contains the student details and a pointer to the next node.


The program is menu-driven and allows the user to:

Add a new student

Display all students

Search a student by roll number

Update student details

Delete a student record

This project demonstrates the use of structures, pointers, dynamic memory allocation, and linked list operations.

3. Objectives

To manage student data efficiently using linked lists.

To understand and apply dynamic memory allocation in C.

To perform operations such as insertion, deletion, search, and update on a linked list.

To develop a simple menu-driven application.

To provide a practical example of using data structures in real-world applications.

4. Methodology

Define a structure for storing student information and a pointer to the next node.

Create a linked list by keeping a head pointer that points to the first student.

Write functions to add, display, search, update, and delete student records.

Take user input through a menu to choose the operation.

Perform actions on the linked list based on the user's choice.

5. Algorithms
Algorithm for Adding a Student

Create a new node.

Input student details.

Point the new node to the current head.

Make the new node the new head.

Algorithm for Displaying Students

Start from the head node.

Print each student's details.

Move to the next node until the end.

Algorithm for Searching a Student

Input the roll number to search.

Traverse the list while comparing roll numbers.

If a match is found, display the details.

If not found, show a message.

Algorithm for Deleting a Student

Input roll number to delete.

Traverse the list using two pointers: current and previous.

If roll matches, adjust links and free memory.

If not found, show a message.

#CODE
/* P3.1 Program of single linked list of non integer type node*/


#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct student {
    int roll_no;
    char name[100];
    float marks;
    struct student *next;
} node;

node* create_list();
void display(node *);
void count(node *);
void search(node *, int);
node* addatbeg(node *);
node* addatend(node *);
node* addafter(node *, int);
node* addbefore(node *, int);
node* addatpos(node *, int);
node* del(node *, int);
node* reverse(node *);
node* getnode();
void flush_input();

int main() {
    int choice, data, item, pos;
    node *start = NULL;

    do {
        printf("\n===== STUDENT RECORD MANAGEMENT SYSTEM =====\n");
        printf("1. Create List\n");
        printf("2. Display\n");
        printf("3. Count\n");
        printf("4. Search\n");
        printf("5. Add at beginning\n");
        printf("6. Add at end\n");
        printf("7. Add after roll no\n");
        printf("8. Add before roll no\n");
        printf("9. Add at position\n");
        printf("10. Delete\n");
        printf("11. Reverse\n");
        printf("12. Quit\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch(choice) {
            case 1:
                start = create_list();
                break;
            case 2:
                display(start);
                break;
            case 3:
                count(start);
                break;
            case 4:
                printf("Enter roll number to search: ");
                scanf("%d", &data);
                search(start, data);
                break;
            case 5:
                start = addatbeg(start);
                break;
            case 6:
                start = addatend(start);
                break;
            case 7:
                printf("Enter roll number after which to insert: ");
                scanf("%d", &item);
                start = addafter(start, item);
                break;
            case 8:
                printf("Enter roll number before which to insert: ");
                scanf("%d", &item);
                start = addbefore(start, item);
                break;
            case 9:
                printf("Enter position to insert: ");
                scanf("%d", &pos);
                start = addatpos(start, pos);
                break;
            case 10:
                printf("Enter roll number to delete: ");
                scanf("%d", &data);
                start = del(start, data);
                break;
            case 11:
                start = reverse(start);
                break;
            case 12:
                exit(0);
            default:
                printf("Invalid choice\n");
        }
    } while(choice != 12);

    return 0;
}

node* getnode() {
    node *temp = (node*)malloc(sizeof(node));
    temp->next = NULL;
    return temp;
}

void flush_input() {
    while(getchar() != '\n');
}

node* create_list() {
    int roll;
    float marks;
    char name[100];
    char ans;
    node *start = NULL, *temp = NULL, *newnode;

    do {
        printf("Enter roll number: ");
        scanf("%d", &roll);
        flush_input();

        printf("Enter name: ");
        fgets(name, sizeof(name), stdin);
        name[strcspn(name, "\n")] = '\0';

        printf("Enter marks: ");
        scanf("%f", &marks);

        newnode = getnode();
        newnode->roll_no = roll;
        strcpy(newnode->name, name);
        newnode->marks = marks;

        if(start == NULL) {
            start = newnode;
            temp = start;
        } else {
            temp->next = newnode;
            temp = newnode;
        }

        printf("Add another student? (y/n): ");
        flush_input();
        ans = getchar();

    } while(ans == 'y' || ans == 'Y');

    return start;
}

void display(node *start) {
    node *p = start;

    if(p == NULL) {
        printf("List is empty\n");
        return;
    }

    printf("\n--- Student List ---\n");
    while(p != NULL) {
        printf("%d | %s | %.2f\n", p->roll_no, p->name, p->marks);
        p = p->next;
    }
    printf("\n");
}

void count(node *start) {
    int cnt = 0;
    node *p = start;

    while(p != NULL) {
        cnt++;
        p = p->next;
    }

    printf("Total students: %d\n", cnt);
}

void search(node *start, int data) {
    node *p = start;
    int pos = 1;

    while(p != NULL) {
        if(p->roll_no == data) {
            printf("Roll %d found at position %d\n", data, pos);
            return;
        }
        p = p->next;
        pos++;
    }

    printf("Roll %d not found\n", data);
}

node* addatbeg(node *start) {
    node *newnode = getnode();

    printf("Enter roll number: ");
    scanf("%d", &newnode->roll_no);
    flush_input();

    printf("Enter name: ");
    fgets(newnode->name, 100, stdin);
    newnode->name[strcspn(newnode->name, "\n")] = '\0';

    printf("Enter marks: ");
    scanf("%f", &newnode->marks);

    newnode->next = start;
    return newnode;
}

node* addatend(node *start) {
    node *newnode = getnode(), *p = start;

    printf("Enter roll number: ");
    scanf("%d", &newnode->roll_no);
    flush_input();

    printf("Enter name: ");
    fgets(newnode->name, sizeof(newnode->name), stdin);
    newnode->name[strcspn(newnode->name, "\n")] = '\0';

    printf("Enter marks: ");
    scanf("%f", &newnode->marks);

    if(start == NULL)
        return newnode;

    while(p->next != NULL)
        p = p->next;

    p->next = newnode;
    return start;
}

node* addafter(node *start, int item) {
    node *p = start, *newnode;

    while(p != NULL) {
        if(p->roll_no == item) {
            newnode = getnode();

            printf("Enter roll number: ");
            scanf("%d", &newnode->roll_no);
            flush_input();

            printf("Enter name: ");
            fgets(newnode->name, 100, stdin);
            newnode->name[strcspn(newnode->name, "\n")] = '\0';

            printf("Enter marks: ");
            scanf("%f", &newnode->marks);

            newnode->next = p->next;
            p->next = newnode;
            return start;
        }
        p = p->next;
    }

    printf("Roll not found\n");
    return start;
}

node* addbefore(node *start, int item) {
    if(start == NULL) {
        printf("List is empty\n");
        return start;
    }

    if(start->roll_no == item) {
        return addatbeg(start);
    }

    node *p = start;
    while(p->next != NULL) {
        if(p->next->roll_no == item) {
            node *newnode = getnode();

            printf("Enter roll number: ");
            scanf("%d", &newnode->roll_no);
            flush_input();

            printf("Enter name: ");
            fgets(newnode->name, 100, stdin);
            newnode->name[strcspn(newnode->name, "\n")] = '\0';

            printf("Enter marks: ");
            scanf("%f", &newnode->marks);

            newnode->next = p->next;
            p->next = newnode;
            return start;
        }
        p = p->next;
    }

    printf("Roll not found\n");
    return start;
}

node* addatpos(node *start, int pos) {
    if(pos == 1)
        return addatbeg(start);

    node *p = start;
    int i;

    for(i = 1; i < pos - 1 && p != NULL; i++)
        p = p->next;

    if(p == NULL) {
        printf("Invalid position\n");
        return start;
    }

    node *newnode = getnode();

    printf("Enter roll number: ");
    scanf("%d", &newnode->roll_no);
    flush_input();

    printf("Enter name: ");
    fgets(newnode->name, 100, stdin);
    newnode->name[strcspn(newnode->name, "\n")] = '\0';

    printf("Enter marks: ");
    scanf("%f", &newnode->marks);

    newnode->next = p->next;
    p->next = newnode;

    return start;
}

node* del(node *start, int data) {
    if(start == NULL) {
        printf("List is empty\n");
        return start;
    }

    if(start->roll_no == data) {
        node *tmp = start;
        start = start->next;
        free(tmp);
        return start;
    }

    node *p = start;
    while(p->next != NULL) {
        if(p->next->roll_no == data) {
            node *tmp = p->next;
            p->next = tmp->next;
            free(tmp);
            return start;
        }
        p = p->next;
    }

    printf("Roll not found\n");
    return start;
}

node* reverse(node *start) {
    node *prev = NULL, *current = start, *next = NULL;

    while(current != NULL) {
        next = current->next;
        current->next = prev;
        prev = current;
        current = next;
    }

    return prev;
}



#OUTPUT

<img width="563" height="387" alt="Image" src="https://github.com/user-attachments/assets/012c8aff-bdba-43da-be3c-73fa80e21028" />


<img width="739" height="334" alt="Image" src="https://github.com/user-attachments/assets/8baa5140-69eb-4032-8b32-3ceb529c9ee3" />


<img width="669" height="335" alt="Image" src="https://github.com/user-attachments/assets/100a1c6c-ac4d-4f31-851c-5a9dfaad5502" />


<img width="733" height="211" alt="Image" src="https://github.com/user-attachments/assets/8d07a50b-9ada-4557-a8a8-cce75684b9ec" />


<img width="671" height="384" alt="Image" src="https://github.com/user-attachments/assets/c48e5774-cc19-45f4-9b42-803ace21e902" />
OUTPUT
