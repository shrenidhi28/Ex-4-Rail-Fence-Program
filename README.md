**EX. NO: 5: IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE**

**Name:** Shrenidhi

**Reg No:** 212223040196

**Dept:** CSE

**AIM:**

To write a C program to implement the Rail Fence transposition technique.

**DESCRIPTION:**

In the Rail Fence Cipher, the plaintext is written downwards and diagonally on successive rails of an imaginary fence. When the bottom rail is reached, the direction changes and the text is written upwards until the top rail is reached. This process is repeated until the entire plaintext is written.

The ciphertext is then obtained by reading the characters row by row.

**ALGORITHM:**

**STEP 1:** Read the plaintext from the user.

**STEP 2:** Read the number of rails from the user.

**STEP 3:** Arrange the plaintext in a zigzag pattern across the specified number of rails.

**STEP 4:** Read the characters row-wise from the rail pattern to obtain the ciphertext.

**STEP 5:** Reconstruct the zigzag rail pattern using the ciphertext.

**STEP 6:** Read the characters in the zigzag order to obtain the decrypted plaintext.

**PROGRAM:**

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

void encryptRailFence(char str[], int rails, char encrypted[])
{
    int i, j, len, count, code[100][1000];

    len = strlen(str);

    // Initialize the code array to 0
    for (i = 0; i < rails; i++)
    {
        for (j = 0; j < len; j++)
        {
            code[i][j] = 0;
        }
    }

    count = 0;
    j = 0;

    while (j < len)
    {
        if (count % 2 == 0)
        {
            // Moving down the rails
            for (i = 0; i < rails && j < len; i++)
            {
                code[i][j] = (int)str[j];
                j++;
            }
        }
        else
        {
            // Moving up the rails
            for (i = rails - 2; i > 0 && j < len; i--)
            {
                code[i][j] = (int)str[j];
                j++;
            }
        }

        count++;
    }

    int pos = 0;

    for (i = 0; i < rails; i++)
    {
        for (j = 0; j < len; j++)
        {
            if (code[i][j] != 0)
            {
                encrypted[pos++] = code[i][j];
            }
        }
    }

    encrypted[pos] = '\0';
}

void decryptRailFence(char str[], int rails, char decrypted[])
{
    int i, j, len, count, code[100][1000], pos = 0;

    len = strlen(str);

    // Initialize the code array to 0
    for (i = 0; i < rails; i++)
    {
        for (j = 0; j < len; j++)
        {
            code[i][j] = 0;
        }
    }

    count = 0;
    j = 0;

    while (j < len)
    {
        if (count % 2 == 0)
        {
            for (i = 0; i < rails && j < len; i++)
            {
                code[i][j] = 1;
                j++;
            }
        }
        else
        {
            for (i = rails - 2; i > 0 && j < len; i--)
            {
                code[i][j] = 1;
                j++;
            }
        }

        count++;
    }

    for (i = 0; i < rails; i++)
    {
        for (j = 0; j < len; j++)
        {
            if (code[i][j] == 1)
            {
                code[i][j] = str[pos++];
            }
        }
    }

    pos = 0;
    count = 0;
    j = 0;

    while (j < len)
    {
        if (count % 2 == 0)
        {
            // Moving down the rails
            for (i = 0; i < rails && j < len; i++)
            {
                if (code[i][j] != 0)
                {
                    decrypted[pos++] = code[i][j];
                }

                j++;
            }
        }
        else
        {
            // Moving up the rails
            for (i = rails - 2; i > 0 && j < len; i--)
            {
                if (code[i][j] != 0)
                {
                    decrypted[pos++] = code[i][j];
                }

                j++;
            }
        }

        count++;
    }

    decrypted[pos] = '\0';
}

int main()
{
    char str[1000], encrypted[1000], decrypted[1000];
    int rails;

    printf("Simulating Rail Fence Cipher\n");

    printf("Enter a Secret Message: ");
    fgets(str, sizeof(str), stdin);

    str[strcspn(str, "\n")] = 0;

    printf("Enter number of rails: ");
    scanf("%d", &rails);

    encryptRailFence(str, rails, encrypted);

    printf("Encrypted Message: %s\n", encrypted);

    decryptRailFence(encrypted, rails, decrypted);

    printf("Decrypted Message: %s\n", decrypted);

    return 0;
}
```

**OUTPUT:**

<img width="492" height="297" alt="image" src="https://github.com/user-attachments/assets/e6becc60-73da-4d76-ab04-0c5872ef9b7c" />

**RESULT:**

The Rail Fence Cipher program was implemented successfully in C. The plaintext was encrypted using the specified number of rails, and the program executed successfully.
