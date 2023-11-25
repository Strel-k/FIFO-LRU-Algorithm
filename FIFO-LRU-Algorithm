#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<ctype.h>
#define MAX 1000

void FIFO(int Frames, char input[]);
void LRU(int Frames, char input[]);
void CleanBuffer() { //clears buffers.
    int c;
    while ((c = getchar())!='\n' && c != EOF);
}
void main() {
    int Page_Frames;
    char option = NULL;
    char input[MAX];

    do {
        system("cls");
        printf("Developed by: F. Dave Damon V. Pararuan, Marl Kyle Alexis C. Marcelo, Allyssa Jade Umipig\nBSIT 2-2\n\n");
        printf("Welcome!\n\n[1] FIFO\n[2] LRU\n[3] Exit\n\n\n");
        printf("---> ");
        int choice = 0;
        scanf("%d", &choice);
        switch (choice) {
        case 1: {
            printf("\nEnter how many Page Strings: ");
            scanf("%d", &Page_Frames);
            printf("Enter a Reference String:");
            scanf(" %[^\n]", input);
            if (strlen(input) > Page_Frames) {
                printf("\nUser Input Exceeds Entered Page Frames!\n");
                CleanBuffer();
                break;

            }
            FIFO(Page_Frames, input);
            break;
        }
        case 2: {
            printf("\nEnter how many Page Strings: ");
            scanf("%d", &Page_Frames);
            printf("Enter a Reference String:");
            scanf(" %[^\n]", input);
            if (strlen(input) > Page_Frames) {
                printf("\nUser Input Exceeds Entered Page Frames!\n");
                CleanBuffer();
                break;

            }
            LRU(Page_Frames, input);
            break;
        }
        case 3: {
            printf("\nGoodbye!\n");
            exit(1);
        }
        default: {
            printf("Invalid Output!\n");
            break;
        }
        }

        printf("\n\nDo you wish to Try Again? (Y/N): ");
        scanf(" %c", &option);

    } while (option == 'Y' || option == 'y');
}

void FIFO(int Frames, char input[]) {
    int Page_Faults = 0, Page_Hits = 0, frame[MAX] = { -1 }, index = 0;
    for (int i = 0; i < strlen(input); i++) {
        char reference = input[i];
        int page;
        if (isdigit(reference)) {
            page = input[i] - '0';
        }
        else if (isalpha(reference)) {
            page = toupper(reference) - 'A' + 10;
        }
        else {
            continue;
        }

        int found = 0;
        for (int j = 0; j < Frames; j++) {
            if (frame[j] == page) {
                found = 1;
                Page_Hits++;
                break;
            }
        }
        if (!found) {
            frame[index] = page;
            index = (index + 1) % Frames;
            Page_Faults++;
        }
    }
    printf("\nPage Faults: %d\n", Page_Faults);
    printf("Page Hits: %d\n", Page_Hits);
}

void LRU(int Frames, char input[]) {
    int Page_Faults = 0, Page_Hits = 0, frames[MAX] = { -1 }, Order[MAX] = { 0 }, time = 0;
    int page = 0;
    int index[MAX];

    for (int i = 0; i < strlen(input); i++) {

        char reference = input[i];
        if (isdigit(reference)) {
            int page = input[i] - '0';
        }
        else if (isalpha(reference)) {
            page = toupper(reference) - 'A' + 10;
        }
        else {
            continue;
        }

        int found = 0;
        for (int j = 0; j < Frames; j++) {
            if (frames[j] == page) {
                found = 1;
                Page_Hits++;
                Order[j] = ++time;
                break;
            }
        }
        if (!found) {
            int MinOrder = Order[0];
            int MinDex = 0;
            Page_Faults++;
            for (int i = 0; i < Frames; i++) {
                if (Order[i] < MinOrder) {
                    MinOrder = Order[i];
                    MinDex = i;
                }
            }
            frames[MinDex] = page;
            Order[MinDex] = ++time;
        }
    }

    printf("\n");
    printf("\nPage Faults: %d", Page_Faults);
    printf("\nPage Hits: %d", Page_Hits);
}
