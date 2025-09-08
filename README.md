# C_programs

# 1) Formatted I/O + operators & expressions

```
/* Use of formatted I/O and basic operators */
#include <stdio.h>
#include <conio.h>

void main() {
    int a, b;
    float avg;
    clrscr();

    /* Step 1: Input two integers */
    printf("Enter two integers: ");
    scanf("%d %d", &a, &b);

    /* Step 2: Apply operators */
    printf("Sum        = %d\n", a + b);
    printf("Difference = %d\n", a - b);
    printf("Product    = %d\n", a * b);
    printf("Quotient   = %d\n", b != 0 ? a / b : 0);
    printf("Remainder  = %d\n", b != 0 ? a % b : 0);

    /* Step 3: Expression with type cast */
    avg = (a + b) / 2.0;
    printf("Average    = %.2f\n", avg);

    getch();
}
```
#  2) Control structures (selection/decision)
(A) If-else ladder: Grade calculator
```
#include <stdio.h>
#include <conio.h>

void main() {
    int m;
    clrscr();

    printf("Enter marks (0-100): ");
    scanf("%d", &m);

    if (m >= 90)        printf("Grade: A+\n");
    else if (m >= 75)   printf("Grade: A\n");
    else if (m >= 60)   printf("Grade: B\n");
    else if (m >= 40)   printf("Grade: C\n");
    else                printf("Grade: Fail\n");

    getch();
}
```
# (B) Switch-case: Day of week
```
#include <stdio.h>
#include <conio.h>

void main() {
    int d;
    clrscr();

    printf("Enter 1-7: ");
    scanf("%d", &d);

    switch(d) {
        case 1: printf("Monday\n"); break;
        case 2: printf("Tuesday\n"); break;
        case 3: printf("Wednesday\n"); break;
        case 4: printf("Thursday\n"); break;
        case 5: printf("Friday\n"); break;
        case 6: printf("Saturday\n"); break;
        case 7: printf("Sunday\n"); break;
        default: printf("Invalid!\n");
    }
    getch();
}
```
# 3) Functions (modularity) – Prime check using a function
```
#include <stdio.h>
#include <conio.h>

int isPrime(int n) {
    int i;
    if (n < 2) return 0;
    for (i = 2; i*i <= n; i++)
        if (n % i == 0) return 0;
    return 1;
}

void main() {
    int n;
    clrscr();

    printf("Enter a number: ");
    scanf("%d", &n);

    if (isPrime(n)) printf("%d is PRIME\n", n);
    else            printf("%d is NOT prime\n", n);

    getch();
}
```
# 4) One-dimensional array – Sum, average, min, max
```
#include <stdio.h>
#include <conio.h>

void main() {
    int a[50], n, i, sum = 0, min, max;
    float avg;
    clrscr();

    printf("How many elements (<=50)? ");
    scanf("%d", &n);

    printf("Enter %d integers:\n", n);
    for (i = 0; i < n; i++) {
        scanf("%d", &a[i]);
        sum += a[i];
    }

    min = max = a[0];
    for (i = 1; i < n; i++) {
        if (a[i] < min) min = a[i];
        if (a[i] > max) max = a[i];
    }
    avg = (float)sum / n;

    printf("Sum=%d  Avg=%.2f  Min=%d  Max=%d\n", sum, avg, min, max);
    getch();
}
```
# 5) Two-dimensional array – Matrix addition
```
#include <stdio.h>
#include <conio.h>

void main() {
    int A[5][5], B[5][5], C[5][5];
    int r, c, i, j;
    clrscr();

    printf("Enter rows and cols (<=5): ");
    scanf("%d %d", &r, &c);

    printf("Enter matrix A:\n");
    for (i=0;i<r;i++)
        for (j=0;j<c;j++)
            scanf("%d",&A[i][j]);

    printf("Enter matrix B:\n");
    for (i=0;i<r;i++)
        for (j=0;j<c;j++)
            scanf("%d",&B[i][j]);

    for (i=0;i<r;i++)
        for (j=0;j<c;j++)
            C[i][j] = A[i][j] + B[i][j];

    printf("A + B =\n");
    for (i=0;i<r;i++) {
        for (j=0;j<c;j++) printf("%4d", C[i][j]);
        printf("\n");
    }
    getch();
}
```
# 6) Recursion – Factorial (n!)
```
#include <stdio.h>
#include <conio.h>

long fact(int n) {
    if (n == 0) return 1;     /* base case */
    return n * fact(n - 1);   /* recursive step */
}

void main() {
    int n;
    clrscr();

    printf("Enter n: ");
    scanf("%d", &n);

    printf("Factorial = %ld\n", fact(n));
    getch();
}
```
# 7) Text processing – Count vowels, consonants, digits, spaces
```
#include <stdio.h>
#include <conio.h>
#include <string.h>
#include <ctype.h>

void main() {
    char s[200];
    int i, v=0, c=0, d=0, sp=0, other=0;
    clrscr();

    printf("Enter a line: ");
    gets(s);  /* OK in Turbo C for quick labs */

    for (i=0; s[i]!='\0'; i++) {
        char ch = s[i];
        if (isalpha(ch)) {
            char x = tolower(ch);
            if (x=='a'||x=='e'||x=='i'||x=='o'||x=='u') v++;
            else c++;
        } else if (isdigit(ch)) d++;
        else if (ch==' ' || ch=='\t') sp++;
        else other++;
    }

    printf("Vowels=%d Consonants=%d Digits=%d Spaces=%d Other=%d\n",
           v,c,d,sp,other);
    getch();
}
```
# 8) Structures – Student total, average, grade
```
#include <stdio.h>
#include <conio.h>

struct Student {
    int roll;
    char name[25];
    float m1, m2, m3;
};

char grade(float avg) {
    if (avg >= 75) return 'A';
    else if (avg >= 60) return 'B';
    else if (avg >= 40) return 'C';
    else return 'F';
}

void main() {
    struct Student s;
    float total, avg;
    clrscr();

    printf("Roll, Name, Marks3: ");
    scanf("%d", &s.roll);
    fflush(stdin);          /* works in Turbo C */
    gets(s.name);
    scanf("%f %f %f", &s.m1, &s.m2, &s.m3);

    total = s.m1 + s.m2 + s.m3;
    avg   = total / 3.0;

    printf("\nRoll:%d  Name:%s\nTotal:%.2f  Avg:%.2f  Grade:%c\n",
           s.roll, s.name, total, avg, grade(avg));
    getch();
}
```
# 9) Pointers – Swap using call-by-reference
```
#include <stdio.h>
#include <conio.h>

void swap(int *x, int *y) {
    int t = *x; *x = *y; *y = t;
}

void main() {
    int a, b;
    clrscr();

    printf("Enter a and b: ");
    scanf("%d %d", &a, &b);

    swap(&a, &b);

    printf("After swap: a=%d b=%d\n", a, b);
    getch();
}
```
# 10) Files – Count characters, words, lines
```
#include <stdio.h>
#include <conio.h>

void main() {
    FILE *fp;
    char fname[50];
    int ch, chars=0, words=0, lines=0, inword=0;
    clrscr();

    printf("Enter file name (e.g., input.txt): ");
    scanf("%s", fname);

    fp = fopen(fname, "r");
    if (fp == NULL) {
        printf("Cannot open file!\n");
        getch();
        return;
    }

    while ((ch = fgetc(fp)) != EOF) {
        chars++;
        if (ch == '\n') lines++;
        if (ch==' ' || ch=='\n' || ch=='\t') inword = 0;
        else if (!inword) { inword = 1; words++; }
    }
    fclose(fp);

    printf("Chars=%d  Words=%d  Lines=%d\n", chars, words, lines);
    getch();
}
```
