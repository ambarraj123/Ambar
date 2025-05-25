# Ambarimport java.util.*;

class Car {
    private String carId;
    private String model;
    private double pricePerDay;
    private boolean isAvailable;

    public Car(String carId, String model, double pricePerDay) {
        this.carId = carId;
        this.model = model;
        this.pricePerDay = pricePerDay;
        this.isAvailable = true;
    }

    public String getCarId() {
        return carId;
    }

    public String getModel() {
        return model;
    }

    public double getPricePerDay() {
        return pricePerDay;
    }

    public boolean isAvailable() {
        return isAvailable;
    }

    public void rent() {
        isAvailable = false;
    }

    public void returned() {
        isAvailable = true;
    }

    public void displayInfo() {
        System.out.println("Car ID: " + carId + " | Model: " + model + " | Price per Day: ₹" + pricePerDay + " | Available: " + (isAvailable ? "Yes" : "No"));
    }
}

class RentalSystem {
    private ArrayList<Car> carList;

    public RentalSystem() {
        carList = new ArrayList<>();
    }

    public void addCar(Car car) {
        carList.add(car);
        System.out.println("Car added successfully!");
    }

    public void removeCar(String carId) {
        for (Car car : carList) {
            if (car.getCarId().equalsIgnoreCase(carId)) {
                carList.remove(car);
                System.out.println("Car removed successfully!");
                return;
            }
        }
        System.out.println("Car not found.");
    }

    public void viewAvailableCars() {
        boolean found = false;
        for (Car car : carList) {
            if (car.isAvailable()) {
                car.displayInfo();
                found = true;
            }
        }
        if (!found) {
            System.out.println("No cars available.");
        }
    }

    public void rentCar(String carId) {
        for (Car car : carList) {
            if (car.getCarId().equalsIgnoreCase(carId)) {
                if (car.isAvailable()) {
                    car.rent();
                    System.out.println("Car rented successfully!");
                    return;
                } else {
                    System.out.println("Car is already rented.");
                    return;
                }
            }
        }
        System.out.println("Car not found.");
    }

    public void returnCar(String carId) {
        for (Car car : carList) {
            if (car.getCarId().equalsIgnoreCase(carId)) {
                if (!car.isAvailable()) {
                    car.returned();
                    System.out.println("Car returned successfully!");
                    return;
                } else {
                    System.out.println("Car was not rented.");
                    return;
                }
            }
        }
        System.out.println("Car not found.");
    }

    public void viewAllCars() {
        for (Car car : carList) {
            car.displayInfo();
        }
    }
}

public class CarRentalMain {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        RentalSystem rentalSystem = new RentalSystem();

        // Sample Cars
        rentalSystem.addCar(new Car("C101", "Hyundai i20", 1500));
        rentalSystem.addCar(new Car("C102", "Honda City", 2000));
        rentalSystem.addCar(new Car("C103", "Toyota Innova", 2500));

        int choice;
        do {
            System.out.println("\n=== Car Rental System ===");
            System.out.println("1. View Available Cars");
            System.out.println("2. Rent a Car");
            System.out.println("3. Return a Car");
            System.out.println("4. Admin - Add Car");
            System.out.println("5. Admin - Remove Car");
            System.out.println("6. View All Cars");
            System.out.println("0. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();
            sc.nextLine(); // consume newline

            switch (choice) {
                case 1:
                    rentalSystem.viewAvailableCars();
                    break;
                case 2:
                    System.out.print("Enter Car ID to rent: ");
                    String rentId = sc.nextLine();
                    rentalSystem.rentCar(rentId);
                    break;
                case 3:
                    System.out.print("Enter Car ID to return: ");
                    String returnId = sc.nextLine();
                    rentalSystem.returnCar(returnId);
                    break;
                case 4:
                    System.out.print("Enter Car ID: ");
                    String newId = sc.nextLine();
                    System.out.print("Enter Model: ");
                    String model = sc.nextLine();
                    System.out.print("Enter Price Per Day: ");
                    double price = sc.nextDouble();
                    rentalSystem.addCar(new Car(newId, model, price));
                    break;
                case 5:
                    System.out.print("Enter Car ID to remove: ");
                    String removeId = sc.nextLine();
                    rentalSystem.removeCar(removeId);
                    break;
                case 6:
                    rentalSystem.viewAllCars();
                    break;
                case 0:
                    System.out.println("Thank you for using Car Rental System.");
                    break;
                default:
                    System.out.println("Invalid choice.");
            }
        } while (choice != 0);

        sc.close();
    }
}
