# Random-password-generator
To create a password generator app in C.
C Code Implementation:









#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SPECIAL_CHARS "!@#$%^&*()-_+=<>?"

// Function to generate a random password
void generatePassword(int length, int includeAlphabets, int includeNumbers, int includeSpecialChars) {
    char alphabetLower[] = "abcdefghijklmnopqrstuvwxyz";
    char alphabetUpper[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    char numbers[] = "0123456789";
    char special[] = SPECIAL_CHARS;

    // Create an empty character pool
    char pool[100];
    int poolIndex = 0;

    // Add appropriate characters to the pool based on user selections
    if (includeAlphabets) {
        for (int i = 0; i < 26; i++) {
            pool[poolIndex++] = alphabetLower[i];  // Add lowercase
            pool[poolIndex++] = alphabetUpper[i];  // Add uppercase
        }
    }
    if (includeNumbers) {
        for (int i = 0; i < 10; i++) {
            pool[poolIndex++] = numbers[i];
        }
    }
    if (includeSpecialChars) {
        for (int i = 0; special[i] != '\0'; i++) {
            pool[poolIndex++] = special[i];
        }
    }

    // If no character types are selected, show an error and return
    if (poolIndex == 0) {
        printf("Error: No character types selected!\n");
        return;
    }

    // Seed the random number generator
    srand(time(NULL));

    // Generate a password using the pool of characters
    printf("Generated Password: ");
    for (int i = 0; i < length; i++) {
        int randomIndex = rand() % poolIndex;
        printf("%c", pool[randomIndex]);
    }
    printf("\n");
}

int main() {
    int length;
    int includeAlphabets, includeNumbers, includeSpecialChars;

    // Get the length of the password
    printf("Enter the length of the password: ");
    scanf("%d", &length);

    // Get user preferences for the character set
    printf("Include Alphabets (1 for Yes, 0 for No): ");
    scanf("%d", &includeAlphabets);

    printf("Include Numbers (1 for Yes, 0 for No): ");
    scanf("%d", &includeNumbers);

    printf("Include Special Characters (1 for Yes, 0 for No): ");
    scanf("%d", &includeSpecialChars);

    // Generate and display the password
    generatePassword(length, includeAlphabets, includeNumbers, includeSpecialChars);

    return 0;
}
