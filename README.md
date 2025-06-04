# Ex-6-IMPLEMENTATION-OF-THE-BACK-END-OF-THE-COMPILER-
IMPLEMENTATION OF THE BACK END OF THE COMPILER 
# Date :30/05/2025
# name : karthick v
# Aim :
To write a program to implement the back end of the compiler.
# ALGORITHM
1. Start the program.
2. Get the three variables from statements and stored in the text file k.txt.
3. Compile the program and give the path of the source file.
4. Execute the program.
5. Target code for the given statement is produced.
6. Stop the program.
# PROGRAM
input file:
```
t1 = a + b
t2 = t1 * c
t3 = t2 - d
t4 = t3 / e
x = t4
```
program file:
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
    char line[100], op1[20], op2[20], res[20], op;
    char filename[50];
    FILE *fp;
    int reg = 0;

    printf("Enter the filename of the intermediate code: ");
    scanf("%s", filename);

    fp = fopen(filename, "r");
    if (fp == NULL) {
        printf("Error: Could not open file '%s'.\n", filename);
        return 1;
    }

    printf("\nIntermediate Code:\n\n");
    while (fgets(line, sizeof(line), fp)) {
        printf("\t\t%s", line);
    }

    rewind(fp);

    printf("\n\n\tStatement\t\tTarget Code\n\n");

    while (fgets(line, sizeof(line), fp)) {
        line[strcspn(line, "\n")] = 0;

        if (line[0] == '\0') continue;

        if (sscanf(line, "%s = %s %c %s", res, op1, &op, op2) == 4) {
            printf("\t%s\t\tMOV %s, R%d\n", line, op2, reg);
            printf("\t\t\t\t");
            switch (op) {
                case '+': printf("ADD "); break;
                case '-': printf("SUB "); break;
                case '*': printf("MUL "); break;
                case '/': printf("DIV "); break;
                default:  printf("UNK "); break;
            }
            printf("%s, R%d\n\n", op1, reg);
            reg++;
        } else if (sscanf(line, "%s = %s", res, op1) == 2) {
            printf("\t%s\t\tMOV %s, R%d\n\n", line, op1, reg);
            reg++;
        }
    }

    fclose(fp);
    return 0;
}
```
# OUTPUT
![image](https://github.com/user-attachments/assets/d9da6fde-d534-4314-8970-e854d7da6362)

# Result
The back end of the compiler is implemented successfully, and the output is verified.
