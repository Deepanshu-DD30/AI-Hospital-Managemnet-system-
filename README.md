#include <stdio.h>
#include <string.h>

#define MAX 100

// Structure for patient details
struct Patient {
    int id;
    char name[50];
    int age;
    char gender[10];
    char disease[100];
    char doctor[50];
};

struct Patient p[MAX];
int count = 0;

// Function declarations
void addPatient();
void viewPatients();
void searchPatient();
void aiAssistant();
void assignDoctor(char *disease, char *doctor);

int main() {
    int choice;

    printf("\n===== AI HOSPITAL MANAGEMENT SYSTEM =====\n");

    while (1) {
        printf("\n1. Add Patient");
        printf("\n2. View All Patients");
        printf("\n3. Search Patient by ID");
        printf("\n4. AI Diagnosis Assistant");
        printf("\n5. Exit");
        printf("\nEnter your choice: ");
        scanf("%d", &choice);
        getchar();

        switch (choice) {
            case 1: addPatient(); break;
            case 2: viewPatients(); break;
            case 3: searchPatient(); break;
            case 4: aiAssistant(); break;
            case 5: printf("\nThank you! Stay healthy.\n"); return 0;
            default: printf("\nInvalid choice. Try again!\n");
        }
    }
    return 0;
}

// Add a new patient
void addPatient() {
    if (count >= MAX) {
        printf("\nNo more patients can be added.\n");
        return;
    }

    struct Patient newP;
    newP.id = count + 1;

    printf("\nEnter name: ");
    fgets(newP.name, 50, stdin);
    newP.name[strcspn(newP.name, "\n")] = 0;

    printf("Enter age: ");
    scanf("%d", &newP.age);
    getchar();

    printf("Enter gender: ");
    fgets(newP.gender, 10, stdin);
    newP.gender[strcspn(newP.gender, "\n")] = 0;

    printf("Enter disease/symptoms: ");
    fgets(newP.disease, 100, stdin);
    newP.disease[strcspn(newP.disease, "\n")] = 0;

    assignDoctor(newP.disease, newP.doctor);

    p[count++] = newP;
    printf("\nPatient added successfully!\nAssigned Doctor: %s\n", newP.doctor);
}

// View all patients
void viewPatients() {
    if (count == 0) {
        printf("\nNo patients available.\n");
        return;
    }

    printf("\n--- PATIENT LIST ---\n");
    for (int i = 0; i < count; i++) {
        printf("\nID: %d", p[i].id);
        printf("\nName: %s", p[i].name);
        printf("\nAge: %d", p[i].age);
        printf("\nGender: %s", p[i].gender);
        printf("\nDisease: %s", p[i].disease);
        printf("\nDoctor: %s\n", p[i].doctor);
    }
}

// Search a patient by ID
void searchPatient() {
    int id, found = 0;
    printf("\nEnter Patient ID: ");
    scanf("%d", &id);

    for (int i = 0; i < count; i++) {
        if (p[i].id == id) {
            printf("\n--- PATIENT DETAILS ---\n");
            printf("Name: %s\nAge: %d\nGender: %s\nDisease: %s\nDoctor: %s\n",
                   p[i].name, p[i].age, p[i].gender, p[i].disease, p[i].doctor);
            found = 1;
            break;
        }
    }
    if (!found)
        printf("\nPatient not found!\n");
}

// Assign doctor based on disease keywords (simple AI logic)
void assignDoctor(char *disease, char *doctor) {
    if (strstr(disease, "fever") || strstr(disease, "cold") || strstr(disease, "flu"))
        strcpy(doctor, "Dr. Smith (General Physician)");
    else if (strstr(disease, "heart") || strstr(disease, "chest"))
        strcpy(doctor, "Dr. Brown (Cardiologist)");
    else if (strstr(disease, "skin") || strstr(disease, "rash"))
        strcpy(doctor, "Dr. Patel (Dermatologist)");
    else if (strstr(disease, "eye") || strstr(disease, "vision"))
        strcpy(doctor, "Dr. Lee (Ophthalmologist)");
    else if (strstr(disease, "child") || strstr(disease, "baby"))
        strcpy(doctor, "Dr. Adams (Pediatrician)");
    else
        strcpy(doctor, "Dr. Taylor (General Specialist)");
}

// AI Diagnosis Assistant
void aiAssistant() {
    char symptoms[100];
    printf("\nEnter symptoms: ");
    getchar();
    fgets(symptoms, 100, stdin);
    symptoms[strcspn(symptoms, "\n")] = 0;

    printf("\n--- AI Diagnosis Result ---\n");

    if (strstr(symptoms, "fever") && strstr(symptoms, "cough"))
        printf("Possible: Flu or Viral Infection\nDoctor: General Physician\n");
    else if (strstr(symptoms, "chest") && strstr(symptoms, "pain"))
        printf("Possible: Heart Issue\nDoctor: Cardiologist\n");
    else if (strstr(symptoms, "skin") && strstr(symptoms, "itch"))
        printf("Possible: Skin Allergy\nDoctor: Dermatologist\n");
    else if (strstr(symptoms, "eye") && strstr(symptoms, "red"))
        printf("Possible: Eye Infection\nDoctor: Ophthalmologist\n");
    else
        printf("Condition unclear. Visit General Specialist.\n");
}
# AI-Hospital-Managemnet-system-