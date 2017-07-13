# Singly Linked List

```c
#include <stdio.h>
#include <stdlib.h>

#define TRUE		1
#define FALSE		0

//Singly linked list.

typedef struct Node {
	int data;
	struct Node* link;
}NODE;

int createNode(NODE* head, int data);
int deleteNode(NODE* head, int position);
int getLinkedLength(NODE* head);
void displayLinkedList(NODE* head);

int main() {

	NODE* head = NULL;
	int input;
	int position;
	int data;

	head = (NODE*)malloc(sizeof(NODE));
	if (head != NULL) {
		memset(head, 0, sizeof(NODE));
		head->link = NULL;
	}
	else {
		printf("Error, memory allocation main(), head \n");
		return FALSE;
	}
	while (1) {
		printf("1 = Create Node, 2 = Delete Node, 3 = Display Linked List, 4 = Exit.\nWhat do you want? = ");
		scanf("%d", &input);
		switch (input) {
		case 1:
			printf("Input data = ");
			scanf("%d", &data);
			createNode(head, data);
			break;
		case 2:
			printf("Input position = ");
			scanf("%d", &position);
			deleteNode(head, position);
			break;
		case 3:
			displayLinkedList(head);
			break;
		case 4:
			exit(1);
			break;
		default:
			printf("Error, Wrong Input.");
		}
	}

	return 0;
}
int createNode(NODE* head, int data) {

	int ret = FALSE;
	NODE* newNode = NULL; 
	NODE* p = head;
	

	newNode = (NODE*)malloc(sizeof(NODE));
	if (newNode != NULL) {
		while (p->link != NULL) {
			p = p->link;
		}
		p->link = newNode;
		newNode->data = data;
		newNode->link = NULL;

		ret = TRUE;
	}
	else {
		printf("Error, Memory Allocation, createNode()\n");
		return ret;
	}
	
	return ret;

}
int deleteNode(NODE* head, int position) {

	int ret = FALSE;
	NODE* p = head;
	NODE* pre = NULL;

	if (position <= getLinkedLength) {
		
		for (int i = 0; i < position; i++) {
			pre = p;
			p = p->link;
		}

		pre->link = p->link;
		free(p);

		ret = TRUE;

	}
	else {
		printf("Error, Wrong position, deleteNode()\n");
		return ret;
	}

	return ret;
}
int getLinkedLength(NODE* head) {

	int ret = 0;

	NODE* p = head;
	
	while (p->link != NULL) {
		p = p->link;
		ret++;
	}

	return ret;

}
void displayLinkedList(NODE* head) {

	int index = 0;
	NODE* p = head;

	while (p->link != NULL) {
		p = p->link;
		printf("[%d]:%d\n",index,p->data);
		index++;
	}
}

```