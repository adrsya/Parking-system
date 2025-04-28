//# Parking-system
//In c language 
#include <stdio.h>
#include <string.h>

#define MAX_VEHICLES 100

typedef struct {
    char type[20];
    char arrivalTime[10];
} Vehicle;

Vehicle vehicles[MAX_VEHICLES];
int totalVehicles = 0;
int totalCars = 0;
int totalTricycles = 0;

// Function to add a vehicle
void arrival() {
    if (totalVehicles >= MAX_VEHICLES) {
        printf("Parking full!\n");
        return;
    }
    
    printf("Enter vehicle type (Car/Tricycle/Other): ");
    scanf("%s", vehicles[totalVehicles].type);

    printf("Enter arrival time (HH:MM): ");
    scanf("%s", vehicles[totalVehicles].arrivalTime);

    if (strcmp(vehicles[totalVehicles].type, "Car") == 0 || strcmp(vehicles[totalVehicles].type, "car") == 0)
        totalCars++;
    else if (strcmp(vehicles[totalVehicles].type, "Tricycle") == 0 || strcmp(vehicles[totalVehicles].type, "tricycle") == 0)
        totalTricycles++;

    totalVehicles++;

    printf("Vehicle parked successfully.\n");
}

// Function to show total vehicles
void showTotalVehicles() {
    printf("Total vehicles parked: %d\n", totalVehicles);
}

// Function to show total cars
void showTotalCars() {
    printf("Total cars parked: %d\n", totalCars);
}

// Function to show total tricycles
void showTotalTricycles() {
    printf("Total tricycles parked: %d\n", totalTricycles);
}

// Function to display all vehicles
void displayVehicles() {
    printf("Vehicles parked in order:\n");
    for (int i = 0; i < totalVehicles; i++) {
        printf("%d. Type: %s, Arrival Time: %s\n", i+1, vehicles[i].type, vehicles[i].arrivalTime);
    }
}

// Function to remove a vehicle
void departure() {
    if (totalVehicles == 0) {
        printf("No vehicles to depart.\n");
        return;
    }

    int vehicleNumber;
    printf("Enter vehicle number to depart (1 to %d): ", totalVehicles);
    scanf("%d", &vehicleNumber);

    if (vehicleNumber < 1 || vehicleNumber > totalVehicles) {
        printf("Invalid vehicle number.\n");
        return;
    }

    vehicleNumber--; // Convert to array index

    if (strcmp(vehicles[vehicleNumber].type, "Car") == 0 || strcmp(vehicles[vehicleNumber].type, "car") == 0)
        totalCars--;
    else if (strcmp(vehicles[vehicleNumber].type, "Tricycle") == 0 || strcmp(vehicles[vehicleNumber].type, "tricycle") == 0)
        totalTricycles--;

    // Shift all vehicles up to fill the gap
    for (int i = vehicleNumber; i < totalVehicles - 1; i++) {
        vehicles[i] = vehicles[i + 1];
    }

    totalVehicles--;

    printf("Vehicle departed successfully.\n");
}

int main() {
    int choice;

    do {
        printf("\n--- Vehicle Parking System ---\n");
        printf("1. Arrival of Parking\n");
        printf("2. Total number of vehicles parked\n");
        printf("3. Total number of cars parked\n");
        printf("4. Total number of tricycles parked\n");
        printf("5. Display order in which vehicles are parked\n");
        printf("6. Departure of vehicle\n");
        printf("7. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: arrival(); break;
            case 2: showTotalVehicles(); break;
            case 3: showTotalCars(); break;
            case 4: showTotalTricycles(); break;
            case 5: displayVehicles(); break;
            case 6: departure(); break;
            case 7: printf("Exiting system...\n"); break;
            default: printf("Invalid choice! Try again.\n");
        }

    } while (choice != 7);

    return 0;
}
