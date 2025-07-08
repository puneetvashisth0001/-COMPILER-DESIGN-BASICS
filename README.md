# -COMPILER-DESIGN-BASICS

*COMPANY NAME* : CODTECH IT SOLUTIONS

*NAME* : PUNEET VASHISTH

*INTERN ID* : CT04DG757

*DOMAIN* : C PROGRAMMING

*MENTOR* : NEELA SANTOSH

*I USE VS CODE*

THE CODE IS :
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

// List of C keywords
const char* keywords[] = {
    "int", "float", "return", "if", "else", "while", "for", "char", "double", "void"
};

int isKeyword(const char* word) {
    for (int i = 0; i < sizeof(keywords)/sizeof(keywords[0]); i++) {
        if (strcmp(word, keywords[i]) == 0)
            return 1;
    }
    return 0;
}

int isOperator(char ch) {
    return ch == '+' || ch == '-' || ch == '*' || ch == '/' || ch == '=' || ch == '<' || ch == '>';
}

int isIdentifierStart(char ch) {
    return isalpha(ch) || ch == '_';
}

int isIdentifierChar(char ch) {
    return isalnum(ch) || ch == '_';
}

void analyzeFile(const char* filename) {
    FILE* fp = fopen(filename, "r");
    if (fp == NULL) {
        perror("Error opening file");
        return;
    }

    char ch;
    char buffer[100];
    int i = 0;

    while ((ch = fgetc(fp)) != EOF) {
        // Skip whitespace
        if (isspace(ch)) {
            continue;
        }

        // Operators
        if (isOperator(ch)) {
            printf("Operator: %c\n", ch);
            continue;
        }

        // Identifiers / Keywords
        if (isIdentifierStart(ch)) {
            buffer[i++] = ch;
            while ((ch = fgetc(fp)) != EOF && isIdentifierChar(ch)) {
                buffer[i++] = ch;
            }
            buffer[i] = '\0';
            i = 0;

            if (isKeyword(buffer))
                printf("Keyword: %s\n", buffer);
            else
                printf("Identifier: %s\n", buffer);

            // Put back the non-identifier character
            if (ch != EOF)
                ungetc(ch, fp);
        }
    }

    fclose(fp);
}

int main() {
    char filename[100];
    printf("Enter the filename to analyze: ");
    scanf("%s", filename);

    analyzeFile(filename);

    return 0;
}

VS CODE OUTPUT IS 
<img width="267" height="198" alt="Image" src="https://github.com/user-attachments/assets/8ee7de79-14a7-4d72-9006-325cef76c973" />
