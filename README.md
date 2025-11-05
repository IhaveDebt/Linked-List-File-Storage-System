#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Node {
    char data[100];
    struct Node *next;
} Node;

Node* createNode(char *data) {
    Node *newNode = (Node*)malloc(sizeof(Node));
    strcpy(newNode->data, data);
    newNode->next = NULL;
    return newNode;
}

void saveToFile(Node *head, char *filename) {
    FILE *fp = fopen(filename, "w");
    while (head) {
        fprintf(fp, "%s\n", head->data);
        head = head->next;
    }
    fclose(fp);
    printf("Data saved to file.\n");
}

void display(Node *head) {
    while (head) {
        printf("%s\n", head->data);
        head = head->next;
    }
}

int main() {
    Node *head = NULL, *temp;
    char input[100];
    int choice;

    while (1) {
        printf("\n1. Add Data\n2. Display\n3. Save to File\n4. Exit\nChoose: ");
        scanf("%d", &choice);
        getchar();

        if (choice == 1) {
            printf("Enter text: ");
            fgets(input, sizeof(input), stdin);
            input[strcspn(input, "\n")] = 0;
            Node *newNode = createNode(input);
            newNode->next = head;
            head = newNode;
        } else if (choice == 2) display(head);
        else if (choice == 3) saveToFile(head, "storage.txt");
        else if (choice == 4) break;
        else printf("Invalid choice.\n");
    }
    return 0;
}
