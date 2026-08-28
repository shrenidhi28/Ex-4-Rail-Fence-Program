# Ex-5 Rail-Fence-Program
## Name: Shrenidhi
## Reg No: 212223040196
## Dept: CSE
# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM

```
#include <stdio.h>
#include <string.h>

int main()
{
    char text[100];
    char rail[10][100];
    int len, rails;
    int i, j;

    printf("Enter a Secret Message: ");
    scanf("%s", text);

    printf("Enter number of rails: ");
    scanf("%d", &rails);

    len = strlen(text);

    // Initialize rail matrix
    for (i = 0; i < rails; i++)
        for (j = 0; j < len; j++)
            rail[i][j] = '\n';

    int row = 0;
    int dir_down = 1;

    // Fill the rail matrix
    for (i = 0; i < len; i++)
    {
        rail[row][i] = text[i];

        if (row == 0)
            dir_down = 1;
        else if (row == rails - 1)
            dir_down = 0;

        if (dir_down)
            row++;
        else
            row--;
    }

    printf("\nEncrypted Message: ");

    // Read the matrix row-wise
    for (i = 0; i < rails; i++)
    {
        for (j = 0; j < len; j++)
        {
            if (rail[i][j] != '\n')
                printf("%c", rail[i][j]);
        }
    }

    printf("\n");

    return 0;
}

```

# OUTPUT
<img width="544" height="410" alt="image" src="https://github.com/user-attachments/assets/a792d0e1-9e65-4a97-bad8-27d1cca8403b" />


# RESULT
The Rail Fence Cipher program was implemented successfully in C. The plaintext was encrypted using the specified number of rails, and the program executed successfully.
