#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define MAX_SIZE_USER_NAME 30
#define MAX_SIZE_PASSWORD 20
#define FILE_HEADER_SIZE  sizeof(sFileHeader)

typedef struct {
    char username[MAX_SIZE_USER_NAME];
    char password[MAX_SIZE_PASSWORD];
} sFileHeader;

 struct Employee{
    int id;
    char name[100];
    char department[100];
    char position[100];
    float salary;
} ;

//FUNCTION DECLARATION


    void addEmployee(struct Employee *employees, int *numEmployees);
    void archieveEmployee(struct Employee *employees, int *numEmployees);
    void viewEmployees(struct Employee *employees, int numEmployees);
    void searchEmployee(struct Employee *employees, int numEmployees);
    void editEmployee(struct Employee *employees, int numEmployees);
    int isFileExists(const char *path);
    void init();

    void printIntroduction();
    void printfEmployeeRecordSystem();
    int findEmployeeIndexByID(struct Employee *employees, int numEmployees, int id);
    int findEmployeeIndexByName(struct Employee *employees, int numEmployees, const char *name);
    void printEmployeeDetails(struct Employee employee);
    void shiftEmployees(struct Employee *employees, int numEmployees, int startIndex);
    void changePassword(sFileHeader *fileHeader);


//MAIN FUNCTION
int main(){

        struct Employee employees[50];
        int numEmployees = 0;
        int choice;

        printIntroduction();

        system("cls");
        sFileHeader fileHeader;
        init();
        login();

        do
        {
            system("cls");
            printfEmployeeRecordSystem();
            printf("\n\n\n\n\n\n\n\n\n\t\t\t\t\t\t                        MENU                 \n");
            printf("\n\t\t\t\t\t\t\t   ==============================");
            printf("\n\t\t\t\t\t\t\t   | 1.ADD EMPLOYEE             |");
            printf("\n\t\t\t\t\t\t\t   | 2.ARCHIEVE EMPLOYEE        |");
            printf("\n\t\t\t\t\t\t\t   | 3.VIEW EMPLOYEE            |");
            printf("\n\t\t\t\t\t\t\t   | 4.SEARCH EMPLOYEE          |");
            printf("\n\t\t\t\t\t\t\t   | 5.EDIT EMPLOYEE            |");
            printf("\n\t\t\t\t\t\t\t   | 6.change password          |");
            printf("\n\t\t\t\t\t\t\t   | 7.Exit                     |");
            printf("\n\t\t\t\t\t\t\t   ==============================\n");
            printf("\n=================================================================================================================================================");
            printf("\n\n\t\t\t\t\t\t\t\tEnter choice (1-5): ");
            scanf("%d", &choice);

            switch (choice)
            {
            case 1:
                addEmployee(employees, &numEmployees);
                break;
            case 2:
                archieveEmployee(employees, &numEmployees);
                break;
            case 3:
                viewEmployees(employees, numEmployees);
                break;
            case 4:
                searchEmployee(employees, numEmployees);
                break;
            case 5:
                editEmployee(employees, numEmployees);
                case 6:
            changePassword(&fileHeader);
            break;
            case 7:
                printf("\n\t\t\t\t\t\t\t\tExiting...\n");
                break;

                printf("\n\t\t\t\t\t\t\t\tInvalid choice. Try again.\n");
            }
        } while (choice != 7);//IF HINDI SIYA EQUAL SA 1-5 MAG EEXIT


    return 0;
}
//FUNCTION FOR ADDING A EMPLOYEE
void addEmployee(struct Employee *employees, int *numEmployees){
                system("cls"); //FOR CLEARSCREEN

                printfEmployeeRecordSystem();

                struct Employee newEmployee;

                printf("\n\n\n\n\n\n\n\n\n\t\t\t\t\t\t\t\tEnter employee ID: ");
                scanf("%d", &newEmployee.id);

                int idTaken; // Flag to indicate if the ID is taken
                            do {
                                idTaken = 0; // Assume ID is not taken initially

                                // Check if the entered ID matches any existing employee ID
                                for (int i = 0; i < *numEmployees; i++) {
                                    if (employees[i].id == newEmployee.id) {
                                        idTaken = 1; // Set flag to indicate ID is taken
                                        break; // Exit the loop since ID is already taken
                                    }
                                }

                                // If the ID is taken, prompt the user to enter another ID
                                if (idTaken) {
                                    printf("\n\t\t\t\t\t\t\t\tID is already taken. Please enter another ID: ");
                                    scanf("%d", &newEmployee.id);
                                }
                            } while (idTaken);

                printf("\n\t\t\t\t\t\t\t\tEnter employee name: ");
                scanf(" %[^\n]s", newEmployee.name);

                printf("\n\t\t\t\t\t\t\t\tEnter employee department: ");
                scanf(" %[^\n]s", newEmployee.department);

                printf("\n\t\t\t\t\t\t\t\tEnter employee position: ");
                scanf(" %[^\n]s", newEmployee.position);

                printf("\n\t\t\t\t\t\t\t\tEnter employee salary: ");
                scanf("%f", &newEmployee.salary);

                employees[*numEmployees] = newEmployee;
                (*numEmployees)++; // ITERATION OF VALUE IN RECORDS
                printf("\n\t\t\t\t\t\t\t\tEmployee added successfully.\n");

                printf("\n\n\t\t\t\t\t\t\t\tPress Enter to continue...");
                        getchar();
                        getchar();
            }

//FUNCTION FOR SEARCHING AN EMPLOYEE
void searchEmployee(struct Employee *employees, int numEmployees){

                int searchID;

                system("cls");

                printfEmployeeRecordSystem();

                printf("\n\n\n\n\n\t\t\t\t\t\t\t\tEnter ID of employee to search for: ");
                scanf("%d", &searchID);

                int found = 0;
                do {

                    // Search for the employee with the given ID
                    for (int i = 0; i < numEmployees; i++) {
                        if (employees[i].id == searchID) {

                            // Print the employee details if found
                            printf("\n\n\n\n\n\t\t\t\t\t\t-----------------------------------------------------------------------------------\n");
                            printf("\n\t\t\t\t\t\t| %-12s | %-15s | %-15s | %-15s | %-10s |\n", "Employee ID", "Name", "Department", "Position", "Salary");
                            printf("\n\t\t\t\t\t\t-----------------------------------------------------------------------------------\n");
                            printf("\n\t\t\t\t\t\t| %-12d | %-15s | %-15s | %-15s | $%-9.2f |\n", employees[i].id, employees[i].name, employees[i].department, employees[i].position, employees[i].salary);
                            printf("\n\t\t\t\t\t\t-----------------------------------------------------------------------------------\n");

                            found = 1; // Set found flag to true
                            break; // Exit the loop since the employee is found
                        }
                    }

                    // If the employee is not found
                    if (!found)
                        {
                        printf("\n\t\t\t\t\t\t\tEmployee with ID %d not found.\n", searchID);

                        char tryAgain;

                        printf("\n\t\t\t\t\t\t\tDo you want to search again? (Y/N): ");
                        scanf(" %c", &tryAgain);

                        // If the user does not want to search again, exit the loop
                        if (tryAgain == 'N' || tryAgain == 'n')
                            {
                            break;
                            }
                            else
                                {

                                // Prompt the user to enter another ID
                                printf("\n\n\n\n\n\t\t\t\t\t\t\t\tEnter ID of the employee to search for: ");
                                scanf("%d", &searchID);
                                }
                        }
                }

                while (!found);

                printf("\n\n\t\t\t\t\t\t\tPress Enter to continue...");
                getchar();
                getchar();
            }

//FUNCTION FOR DELETING A EMPLOYEE
void archieveEmployee(struct Employee *employees, int *numEmployees){
                    system("cls");

                    printfEmployeeRecordSystem();

                    printf("\n\n\n\n\n\n\n\n\n\t\t\t\t\t\t\t\tDelete an Employee\n");
                    printf("\n\t\t\t\t\t\t\t\t--------------------\n");
                    printf("\n\t\t\t\t\t\t\t\t1. Archieve by ID\n");
                    printf("\n\t\t\t\t\t\t\t\t2. Archieve by Name\n");
                    printf("\n\t\t\t\t\t\t\t\t--------------------\n");
                    printf("\n\t\t\t\t\t\t\t\tEnter choice (1-2): ");

                    int choice;
                    scanf("%d", &choice);

                    if (choice == 1) {
                        int deleteID;
                        int found = 0;

                        do {
                            printf("\n\t\t\t\t\t\t\t\tEnter ID of the employee to delete: ");
                            scanf("%d", &deleteID);

                            // Find the employee index by ID
                            int employeeIndex = findEmployeeIndexByID(employees, *numEmployees, deleteID);

                            if (employeeIndex != -1) {
                                // Display employee record
                                printf("\n\t\t\t\t\t\t\t\tEmployee Information:\n");
                                printEmployeeDetails(employees[employeeIndex]);

                                // Confirm deletion
                                char confirmation;
                                printf("\n\t\t\t\t\t\t\t\tAre you sure you want to delete this employee? (Y/N): ");
                                scanf(" %c", &confirmation);

                                if (confirmation == 'Y' || confirmation == 'y') {
                                    // Shift remaining employees to fill the gap
                                    shiftEmployees(employees, *numEmployees, employeeIndex);

                                    (*numEmployees)--;

                                    found = 1;

                                    printf("\n\t\t\t\t\t\t\t\tEmployee deleted successfully.\n");
                                } else {
                                    printf("\n\t\t\t\t\t\t\t\tDeletion canceled.\n");
                                }
                            } else {
                                printf("\n\t\t\t\t\t\t\t\tEmployee with ID %d not found.\n", deleteID);

                                char tryAgain;
                                printf("\n\t\t\t\t\t\t\t\tDo you want to enter the ID again? (Y/N): ");
                                scanf(" %c", &tryAgain);

                                if (tryAgain == 'N' || tryAgain == 'n') {
                                    break;
                                }
                            }
                        } while (!found);
                    } else if (choice == 2) {
                        char deleteName[50];
                        int found = 0;

                        do {
                            printf("\n\t\t\t\t\t\t\t\tEnter the name of the employee to delete: ");
                            scanf(" %[^\n]s", deleteName);

                            // Find the employee index by name
                            int employeeIndex = findEmployeeIndexByName(employees, *numEmployees, deleteName);

                            if (employeeIndex != -1) {
                                // Display employee record
                                printf("\n\t\t\t\t\t\t\t\tEmployee Information:\n");
                                printEmployeeDetails(employees[employeeIndex]);

                                // Confirm deletion
                                char confirmation;
                                printf("\n\t\t\t\t\t\t\t\tAre you sure you want to delete this employee? (Y/N): ");
                                scanf(" %c", &confirmation);

                                if (confirmation == 'Y' || confirmation == 'y') {
                                    // Shift remaining employees to fill the gap
                                    shiftEmployees(employees, *numEmployees, employeeIndex);

                                    (*numEmployees)--;

                                    found = 1;

                                    printf("\n\t\t\t\t\t\t\t\tEmployee deleted successfully.\n");
                                } else {
                                    printf("\n\t\t\t\t\t\t\t\tDeletion canceled.\n");
                                }
                            } else {
                                printf("\n\t\t\t\t\t\t\t\tEmployee with name %s not found.\n", deleteName);

                                char tryAgain;
                                printf("\n\t\t\t\t\t\t\t\tDo you want to enter the name again? (Y/N): ");
                                scanf(" %c", &tryAgain);

                                if (tryAgain == 'N' || tryAgain == 'n') {
                                    break;
                                }
                            }
                        } while (!found);
                    } else {
                        printf("\n\t\t\t\t\t\t\t\tInvalid choice. Please try again.\n");
                    }

                    printf("\n\n\t\t\t\t\t\t\t\tPress Enter to continue...");
                    getchar();
                    getchar();
                }

//FUNCTION FOR VIEWING AN EMPLOYEE
void viewEmployees(struct Employee *employees, int numEmployees){
                            if (numEmployees == 0) {
                                system("cls");
                                printf("\n\n\n\n\n\t\t\t\t\t\tNo employees found.\n");
                                printf("\n\t\t\t\t\t\tPress enter to continue...");
                                getchar();
                                getchar();
                                return;
                            }

                            int currentPage = 1;
                            int totalPages = (numEmployees + 9) / 10; // Calculate the total number of pages

                            while (1) {
                                system("cls");
                                printfEmployeeRecordSystem();

                                printf("\n\n\n\n\n\t\t\t\t\t\t-----------------------------------------------------------------------------------\n");
                                printf("\n\t\t\t\t\t\t| %-12s | %-15s | %-15s | %-15s | %-10s |\n", "Employee ID", "Name", "Department", "Position", "Salary");
                                printf("\n\t\t\t\t\t\t-----------------------------------------------------------------------------------\n");

                                int startIndex = (currentPage - 1) * 10;
                                int endIndex = startIndex + 9;
                                if (endIndex >= numEmployees) {
                                    endIndex = numEmployees - 1;
                                }

                                for (int i = startIndex; i <= endIndex; i++) {
                                    printf("\n\t\t\t\t\t\t| %-12d | %-15s | %-15s | %-15s | $%-9.2f |\n", employees[i].id, employees[i].name, employees[i].department, employees[i].position, employees[i].salary);
                                }

                                printf("\n\t\t\t\t\t\t-----------------------------------------------------------------------------------\n");

                                printf("\n\t\t\t\t\t\tPage %d of %d\n", currentPage, totalPages);
                                printf("\n\t\t\t\t\t\t1. Next Page\n");
                                printf("\t\t\t\t\t\t2. Previous Page\n");
                                printf("\t\t\t\t\t\t3. Back to Main Menu\n");
                                printf("\n\t\t\t\t\t\tEnter choice (1-3): ");

                                int choice;
                                scanf("%d", &choice);

                                if (choice == 1) {
                                    if (currentPage < totalPages) {
                                        currentPage++;
                                    } else {
                                        printf("\n\t\t\t\t\t\tYou have reached the end of the record system.\n");
                                    }
                                } else if (choice == 2) {
                                    if (currentPage > 1) {
                                        currentPage--;
                                    } else {
                                        printf("\n\t\t\t\t\t\tYou are already at the beginning of the record system.\n");
                                    }
                                } else if (choice == 3) {
                                    break;
                                } else {
                                    printf("\n\t\t\t\t\t\tInvalid choice. Please try again.\n");
                                }

                                printf("\n\t\t\t\t\t\tPress enter to continue...");
                                getchar();
                                getchar();
                            }
                        }

//FUNCTION FOR EDITTING DETAILS OF AN EMPLOYEE
void editEmployee(struct Employee *employees, int numEmployees){
                        int editID;
                        system("cls");
                        printfEmployeeRecordSystem();
                        printf("\n\n\n\n\n\t\t\t\t\t\t\t\tEnter ID of employee to edit: ");
                        scanf("%d", &editID);

                        int found = 0;
                        int index = -1; // Variable to store the index of the employee

                        for (int i = 0; i < numEmployees; i++)
                        {
                            if (employees[i].id == editID)
                            {
                                found = 1;
                                index = i; // Store the index of the employee
                                break;
                            }
                        }

                        if (!found)
                        {
                            printf("\n\n\n\n\n\t\t\t\t\t\t\t\tEmployee not found. Try again.\n");
                        }
                        else
                        {
                            char confirm;
                            printf("\n\n\n\n\n\t\t\t\t\t\t\t\tEmployee found. Do you want to edit this employee? (Y/N): ");
                            scanf(" %c", &confirm);

                            if (confirm == 'Y' || confirm == 'y')
                            {
                                int newID;
                                printf("\n\n\t\t\t\t\t\t\t\tEnter new ID: ");
                                scanf("%d", &newID);

                                // Validate if the new ID is already in use
                                int idInUse = 0;
                                for (int i = 0; i < numEmployees; i++)
                                {
                                    if (i != index && employees[i].id == newID)
                                    {
                                        idInUse = 1;
                                        break;
                                    }
                                }

                                if (idInUse)
                                {
                                    printf("\n\n\n\n\n\t\t\t\t\t\t\t\tError: ID already in use. Please choose a different ID.\n");
                                }
                                else
                                {
                                    // Update the employee's details
                                    printf("\n\n\t\t\t\t\t\t\t\tEnter new name: ");
                                    scanf("%s", employees[index].name);

                                    printf("\n\n\t\t\t\t\t\t\t\tEnter new department: ");
                                    scanf("%s", employees[index].department);

                                    printf("\n\n\t\t\t\t\t\t\t\tEnter new position: ");
                                    scanf("%s", employees[index].position);

                                    printf("\n\n\t\t\t\t\t\t\t\tEnter new salary: ");
                                    scanf("%f", &employees[index].salary);

                                    printf("\n\n\n\n\n\t\t\t\t\t\t\t\tEmployee details updated successfully!\n");
                                }
                            }
                            else if (confirm == 'N' || confirm == 'n')
                            {
                                printf("\n\n\n\n\n\t\t\t\t\t\t\t\tEdit canceled. No changes were made.\n");
                            }
                            else
                            {
                                printf("\n\n\n\n\n\t\t\t\t\t\t\t\tInvalid input. Edit canceled.\n");
                            }
                        }
                        printf("\n\t\t\t\t\t\tPress enter to continue...");
                        getchar();
                        getchar();

                    }
void printIntroduction(){
                                        printf("\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n");
                                        printf("\n=================================================================================================================================================\n\n");
                                        printf("\t\t\t\t\t\t    ********************************************\n");
                                        printf("\t\t\t\t\t\t    ****       EMPLOYEE RECORD SYSTEM       ****\n");
                                        printf("\t\t\t\t\t\t    ********************************************\n");
                                        printf("\n\n");
                                        printf("\t\t\t\t\t\t       Welcome to our Employee Record System\n");
                                        printf("\t\t\t\t\t\t          Please press Enter to continue...\n\n");
                                        printf("\n=================================================================================================================================================");
                                        getchar(); // Wait for user input
                                    }
void printfEmployeeRecordSystem(){
                                printf("\n=================================================================================================================================================");
                                printf("\n\n\n\n\n\t\t\t\t\t\t    ********************************************\n");
                                printf("\t\t\t\t\t\t    ****       EMPLOYEE RECORD SYSTEM       ****\n");
                                printf("\t\t\t\t\t\t    ********************************************\n\n");
                                printf("\n=================================================================================================================================================");

                            }
int findEmployeeIndexByID(struct Employee *employees, int numEmployees, int id) {
    for (int i = 0; i < numEmployees; i++) {
        if (employees[i].id == id) {
            return i;  // Found employee, return index
        }
    }
    return -1;  // Employee not found, return -1
}
int findEmployeeIndexByName(struct Employee *employees, int numEmployees, const char *name) {
    for (int i = 0; i < numEmployees; i++) {
        if (strcmp(employees[i].name, name) == 0) {
            return i;  // Found employee, return index
        }
    }
    return -1;  // Employee not found, return -1
}
void printEmployeeDetails(struct Employee employee) {
    printf("\n\t\t\t\t\t\t\t\tID: %d\n", employee.id);
    printf("\t\t\t\t\t\t\t\tName: %s\n", employee.name);
    printf("\t\t\t\t\t\t\t\tDepartment: %s\n", employee.department);
    printf("\t\t\t\t\t\t\t\tPosition: %s\n", employee.position);
    printf("\t\t\t\t\t\t\t\tSalary: %.2f\n", employee.salary);
}
void shiftEmployees(struct Employee *employees, int numEmployees, int startIndex) {
    for (int i = startIndex; i < numEmployees - 1; i++) {
        employees[i] = employees[i + 1];
    }
}
void saveDataToFile(struct Employee *employees, int numEmployees) {
    FILE *file = fopen("c:/FILE/employees.dat", "wb");
    if (file == NULL) {
        printf("\nError opening file. Unable to save data.\n");
        return;
    }

    sFileHeader fileHeader;
    strncpy(fileHeader.username, "admin", MAX_SIZE_USER_NAME);
    strncpy(fileHeader.password, "password", MAX_SIZE_PASSWORD);

    fwrite(&fileHeader, sizeof(sFileHeader), 1, file);
    fwrite(employees, sizeof(struct Employee), numEmployees, file);

    fclose(file);
    printf("\nData saved successfully.\n");

    printf("\nPress Enter to continue...");
    getchar();
    getchar();
}

void loadDataFromFile(struct Employee *employees, int *numEmployees) {
    FILE *file = fopen("employees.dat", "rb");
    if (file == NULL) {
        printf("\nError opening file. Unable to load data.\n");
        return;
    }

    sFileHeader fileHeader;
    fread(&fileHeader, sizeof(sFileHeader), 1, file);

    if (strcmp(fileHeader.username, "admin") != 0 || strcmp(fileHeader.password, "password") != 0) {
        printf("\nInvalid username or password. Unable to load data.\n");
        fclose(file);
        return;
    }

    *numEmployees = fread(employees, sizeof(struct Employee), *numEmployees, file);

    fclose(file);
    printf("\nData loaded successfully.\n");

    printf("\nPress Enter to continue...");
    getchar();
    getchar();
}
void login()
{
    unsigned char userName[MAX_SIZE_USER_NAME] = {0};
    unsigned char password[MAX_SIZE_PASSWORD] = {0};
    int L = 0;
    sFileHeader fileHeaderInfo = {0};
    FILE *fp = NULL;
    printIntroduction("Login");
    fp = fopen("c:/FILE/employees.dat", "rb");
    if (fp == NULL)
    {
        printf("File is not opened\n");
        exit(1);
    }
    fread(&fileHeaderInfo, FILE_HEADER_SIZE, 1, fp);
    fclose(fp);
    do
    {
        printf("\n\n\n\t\t\t\tUsername:");
        fgets(userName, MAX_SIZE_USER_NAME, stdin);
        printf("\n\t\t\t\tPassword:");
        fgets(password, MAX_SIZE_PASSWORD, stdin);
        if ((!strcmp(userName, fileHeaderInfo.username)) && (!strcmp(password, fileHeaderInfo.password)))
        {
            printf("\n\t\t\t\tLogin Successful!\n");
            // Call your menu function here
            break;
        }
        else
        {
            printf("\t\t\t\tLogin Failed. Please enter the correct username and password.\n\n");
            L++;
        }
    } while (L <= 3);
    if (L > 3)
    {
        printIntroduction("Login Failed");
        printf("\t\t\t\tSorry, unknown user.\n");
        getchar();
        system("cls");
    }
}
int isFileExists(const char *path)
{
    // Try to open file
    FILE *fp = fopen(path, "rb");
    int status = 0;
    // If file does not exists
    if (fp != NULL)
    {
        status = 1;
        // File exists hence close file
        fclose(fp);
    }
    return status;
}
void init()
{
    FILE *fp = NULL;
    int status = 0;
    const char defaultUsername[] ="aticleworld\n";
    const char defaultPassword[] ="aticleworld\n";
    sFileHeader fileHeaderInfo = {0};
    status = isFileExists("c:/FILE/employees.dat");
    if(!status)
    {
        //create the binary file
        fp = fopen("c:/FILE/employees.dat","wb");
        if(fp != NULL)
        {
            //Copy default password
            strncpy(fileHeaderInfo.password,defaultPassword,sizeof(defaultPassword));
            strncpy(fileHeaderInfo.username,defaultUsername,sizeof(defaultUsername));
            fwrite(&fileHeaderInfo,FILE_HEADER_SIZE, 1, fp);
            fclose(fp);
        }
    }
}
void changePassword(sFileHeader *fileHeader) {
    char currentPassword[MAX_SIZE_PASSWORD];
    char newPassword[MAX_SIZE_PASSWORD];

    printf("\n\t\t\t\t\t\t\t\tEnter current password: ");
    scanf("%s", currentPassword);

    // Check if the current password matches the stored password
    if (strcmp(currentPassword, fileHeader->password) == 0) {
        printf("\n\t\t\t\t\t\t\t\tEnter new password: ");
        scanf("%s", newPassword);

        // Update the password in the file header
        strcpy(fileHeader->password, newPassword);

        printf("\n\t\t\t\t\t\t\t\tPassword changed successfully.\n");
    } else {
        printf("\n\t\t\t\t\t\t\t\tIncorrect password. Password not changed.\n");
    }

    printf("\n\t\t\t\t\t\t\t\tPress Enter to continue...");
    getchar();
    getchar();
}
