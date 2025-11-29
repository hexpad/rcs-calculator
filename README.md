this program uses the radar wavelength and shape dimensions to calculate radar cross section using standard formulas.


```cpp
// Author: hexpad
// Project: Simple RCS Calculator
// Description: Calculates Radar Cross Section (RCS) for a sphere, flat plate, corner reflector, or cylinder

#include <iostream>
#include <string>
#include <cmath>

class RCSCalculator {
private:
    double wavelength;
    int choice;
    double spRadius;          // Sphere
    double plateLength;       // Flat plate and corner reflector
    double plateWidth;        // Flat plate
    double cyRadius;         // Cylinder
    double cyLength;         // Cylinder

    double sphereRCS() {
        return M_PI * pow(spRadius, 2);
    }

    double flatRCS() {
        return (4 * M_PI * pow(plateLength * plateWidth, 2)) / pow(wavelength, 2);
    }

    double cornerRCS() {
        return (12 * M_PI * pow(plateLength, 4)) / pow(wavelength, 2);
    }

    double cylinderRCS() {
        return (2 * M_PI * cyRadius * pow(cyLength, 2)) / wavelength;
    }

public:
    RCSCalculator(double wl, int ch, double r=0, double l=0, double w=0, double cr=0, double cl=0) {
        wavelength = wl;
        choice = ch;
        spRadius = r;
        plateLength = l;
        plateWidth = w;
        cyRadius = cr;
        cyLength = cl;
    }

    double calculateRCS() {
        if (choice == 1) {
            return sphereRCS();
        } else if (choice == 2) {
            return flatRCS();
        } else if (choice == 3) {
            return cornerRCS();
        } else if (choice == 4) {
            return cylinderRCS();
        } else {
            std::cout << "Invalid shape entered!" << std::endl;
            return -1;
        }
    }
};

int main() {
    double wavelength;
    int choice;
    double radius = 0, length = 0, width = 0;

    std::cout << "Enter radar wavelength in meters: ";
    std::cin >> wavelength;

    std::cout << "Enter shape (sphere=1, flatplate=2, corner=3, cylinder=4): ";
    std::cin >> choice;

    if (choice == 1) {
        std::cout << "Enter sphere radius (meters): ";
        std::cin >> radius;
    } else if (choice == 2) {
        std::cout << "Enter flat plate length (meters): ";
        std::cin >> length;
        std::cout << "Enter flat plate width (meters): ";
        std::cin >> width;
    } else if (choice == 3) {
        std::cout << "Enter corner reflector side length (meters): ";
        std::cin >> length;
    } else if (choice == 4) {
        std::cout << "Enter cylinder radius (meters): ";
        std::cin >> radius;
        std::cout << "Enter cylinder length (meters): ";
        std::cin >> length;
    }

    RCSCalculator rcsCalc(wavelength, choice, radius, length, width, radius, length);
    double rcs = rcsCalc.calculateRCS();

    if (rcs >= 0)
        std::cout << "\nCalculated RCS: " << rcs << " m^2" << std::endl;

    return 0;
}
```


# Example

```cpp
Enter radar wavelength in meters: 0.03
Enter shape (sphere=1, flatplate=2, corner=3, cylinder=4): 1
Enter sphere radius (meters): 0.5

Calculated RCS: 0.785398 m^2
```
