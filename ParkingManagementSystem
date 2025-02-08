import java.time.*;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeParseException;
import java.util.ArrayList;
import java.util.Scanner;

public class ParkingManagementSystem {
    static ArrayList<String> vehicleNumbers = new ArrayList<>();
    static ArrayList<String> vehicleTypes = new ArrayList<>();
    static ArrayList<String> vehicleModels = new ArrayList<>();
    static ArrayList<String> ownerNames = new ArrayList<>();
    static ArrayList<LocalDateTime> entryTimes = new ArrayList<>();
    static ArrayList<LocalDateTime> exitTimes = new ArrayList<>();
    static ArrayList<Double> bills = new ArrayList<>();

    static int bikes = 100;
    static int cars = 250;
    static int bicycles = 78;

    static final double PEAK_BICYCLE_RATE = 7;
    static final double PEAK_BIKE_RATE = 12;
    static final double PEAK_CAR_RATE = 25;
    static final double REGULAR_BICYCLE_RATE = 5;
    static final double REGULAR_BIKE_RATE = 10;
    static final double REGULAR_CAR_RATE = 20;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while (true) {
            System.out.println("----------------------------------------------------------------------------------------");
            System.out.println("\t\t\tParking Management System");
            System.out.println("----------------------------------------------------------------------------------------");
            System.out.println("1. Vehicle Entry");
            System.out.println("2. Remove Entry and Calculate Bill");
            System.out.println("3. View Parked Vehicles");
            System.out.println("4. View Left Parking Space");
            System.out.println("5. Search Parked Vehicle");
            System.out.println("6. Generate Daily Report");
            System.out.println("7. Generate Monthly Report");
            System.out.println("8. Close Program");
            System.out.print("\tSelect option: ");

            int ch;
            try {
                ch = Integer.parseInt(sc.nextLine());
            } catch (NumberFormatException e) {
                System.out.println("###### Please Enter a Valid Number ######");
                continue;
            }

            switch (ch) {
                case 1 -> vehicleEntry(sc);
                case 2 -> removeEntryAndCalculateBill(sc);
                case 3 -> viewParkedVehicles();
                case 4 -> viewLeftParkingSpace();
                case 5 -> searchParkedVehicle(sc);
                case 6 -> generateDailyReport();
                case 7 -> generateMonthlyReport();
                case 8 -> {
                    System.out.println("Thank you for using the Parking Management System.");
                    sc.close();
                    return;
                }
                default -> System.out.println("###### Invalid Option ######");
            }
        }
    }

    private static void vehicleEntry(Scanner sc) {
        String Vno;
        while (true) {
            System.out.print("\tEnter vehicle number (XX-XX-XX-XXXX): ");
            Vno = sc.nextLine().toUpperCase().trim();
            if (Vno.isEmpty()) {
                System.out.println("###### Enter Vehicle Number ######");
            } else if (vehicleNumbers.contains(Vno)) {
                System.out.println("###### Vehicle Number Already Exists ######");
            } else if (Vno.length() == 13 && Vno.matches("^[A-Z]{2}-\\d{2}-[A-Z]{2}-\\d{4}$")) {
                vehicleNumbers.add(Vno);
                break;
            } else {
                System.out.println("###### Enter Valid Vehicle Number ###### (Format: XX-XX-XX-XXXX)");
            }
        }

        String Vtype;
        while (true) {
            System.out.print("\tEnter vehicle type (A for Bicycle | B for Bike | C for Car): ");
            Vtype = sc.nextLine().toUpperCase().trim();
            if (Vtype.equals("A") && bicycles > 0) {
                vehicleTypes.add("Bicycle");
                bicycles--;
                break;
            } else if (Vtype.equals("B") && bikes > 0) {
                vehicleTypes.add("Bike");
                bikes--;
                break;
            } else if (Vtype.equals("C") && cars > 0) {
                vehicleTypes.add("Car");
                cars--;
                break;
            } else {
                System.out.println("###### Invalid Type or No Space Left ######");
            }
        }

        System.out.print("\tEnter vehicle model: ");
        String vname = sc.nextLine().trim();
        vehicleModels.add(vname);

        System.out.print("\tEnter owner name: ");
        String OName = sc.nextLine().trim();
        ownerNames.add(OName);

        LocalDateTime entryTime = LocalDateTime.now();
        entryTimes.add(entryTime);

        System.out.println("Entry recorded. Time: " + entryTime.format(DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss")));
    }

    private static void removeEntryAndCalculateBill(Scanner sc) {
        System.out.print("\tEnter vehicle number to remove: ");
        String Vno = sc.nextLine().toUpperCase().trim();
        if (!vehicleNumbers.contains(Vno)) {
            System.out.println("###### Vehicle Not Found ######");
            return;
        }

        int i = vehicleNumbers.indexOf(Vno);
        LocalDateTime entryTime = entryTimes.get(i);
        LocalDateTime exitTime = LocalDateTime.now();
        Duration duration = Duration.between(entryTime, exitTime);
        double bill = calculateBill(vehicleTypes.get(i), duration, entryTime);

        System.out.println("Receipt for Vehicle Number: " + Vno);
        System.out.println("Entry Time: " + entryTime.format(DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss")));
        System.out.println("Exit Time: " + exitTime.format(DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss")));
        System.out.println("Total Time Parked: " + duration.toHours() + " hours " + duration.toMinutesPart() + " minutes");
        System.out.println("Total Bill: ₹" + bill);

        bills.add(bill);
        exitTimes.add(exitTime);

        switch (vehicleTypes.get(i)) {
            case "Bicycle" -> bicycles++;
            case "Bike" -> bikes++;
            case "Car" -> cars++;
        }

        vehicleNumbers.remove(i);
        vehicleTypes.remove(i);
        vehicleModels.remove(i);
        ownerNames.remove(i);
        entryTimes.remove(i);
    }

    private static double calculateBill(String vehicleType, Duration duration, LocalDateTime entryTime) {
        long totalMinutes = duration.toMinutes();
        long totalHours = duration.toHours();
        double rate = switch (vehicleType) {
            case "Bicycle" -> isPeakHours(entryTime) ? PEAK_BICYCLE_RATE : REGULAR_BICYCLE_RATE;
            case "Bike" -> isPeakHours(entryTime) ? PEAK_BIKE_RATE : REGULAR_BIKE_RATE;
            case "Car" -> isPeakHours(entryTime) ? PEAK_CAR_RATE : REGULAR_CAR_RATE;
            default -> 0;
        };

        if (totalMinutes <= 60) return 0;
        return rate * (totalHours + (duration.toMinutesPart() > 0 ? 1 : 0)) - rate;
    }

    private static boolean isPeakHours(LocalDateTime time) {
        int hour = time.getHour();
        return hour >= 8 && hour <= 20;
    }

    private static void viewParkedVehicles() {
        if (vehicleNumbers.isEmpty()) {
            System.out.println("###### No Vehicles Parked ######");
            return;
        }

        String format = "| %-15s | %-10s | %-15s | %-20s | %-20s |%n";
        System.out.println("+-----------------+------------+-----------------+----------------------+----------------------+");
        System.out.printf("| Vehicle Number  | Type       | Vehicle Model   | Owner Name           | Entry Time           |%n");
        System.out.println("+-----------------+------------+-----------------+----------------------+----------------------+");
        for (int i = 0; i < vehicleNumbers.size(); i++) {
            System.out.printf(format, vehicleNumbers.get(i), vehicleTypes.get(i), vehicleModels.get(i), ownerNames.get(i),
                    entryTimes.get(i).format(DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss")));
        }
        System.out.println("+-----------------+------------+-----------------+----------------------+----------------------+");
    }

    private static void viewLeftParkingSpace() {
        System.out.println("Spaces Left:");
        System.out.println("Bicycles: " + bicycles);
        System.out.println("Bikes: " + bikes);
        System.out.println("Cars: " + cars);
    }

    private static void searchParkedVehicle(Scanner sc) {
        System.out.println("Search By: \n1. Vehicle Number\n2. Owner Name\n3. Entry Time (dd-MM-yyyy)");
        int choice = sc.nextInt();
        sc.nextLine();
        switch (choice) {
            case 1 -> {
                System.out.print("Enter Vehicle Number: ");
                String vehicleNo = sc.nextLine().toUpperCase().trim();
                searchVehicleByNumber(vehicleNo);
            }
            case 2 -> {
                System.out.print("Enter Owner Name: ");
                String ownerName = sc.nextLine().trim();
                searchVehicleByOwner(ownerName);
            }
            case 3 -> {
                System.out.print("Enter Entry Date (dd-MM-yyyy): ");
                String dateInput = sc.nextLine();
                searchVehicleByDate(dateInput);
            }
            default -> System.out.println("###### Invalid Option ######");
        }
    }

    private static void searchVehicleByNumber(String vehicleNo) {
        if (vehicleNumbers.contains(vehicleNo)) {
            int index = vehicleNumbers.indexOf(vehicleNo);
            displayVehicleDetails(index);
        } else {
            System.out.println("###### Vehicle Not Found ######");
        }
    }

    private static void searchVehicleByOwner(String ownerName) {
        if (ownerNames.contains(ownerName)) {
            int index = ownerNames.indexOf(ownerName);
            displayVehicleDetails(index);
        } else {
            System.out.println("###### Owner Not Found ######");
        }
    }

    private static void searchVehicleByDate(String dateInput) {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");
        try {
            LocalDate searchDate = LocalDate.parse(dateInput, formatter);
            boolean found = false;
            for (int i = 0; i < entryTimes.size(); i++) {
                if (entryTimes.get(i).toLocalDate().equals(searchDate)) {
                    displayVehicleDetails(i);
                    found = true;
                }
            }
            if (!found) {
                System.out.println("###### No Entries on Given Date ######");
            }
        } catch (DateTimeParseException e) {
            System.out.println("###### Invalid Date Format ######");
        }
    }

    private static void displayVehicleDetails(int index) {
        System.out.println("Vehicle Number: " + vehicleNumbers.get(index));
        System.out.println("Vehicle Type: " + vehicleTypes.get(index));
        System.out.println("Vehicle Model: " + vehicleModels.get(index));
        System.out.println("Owner Name: " + ownerNames.get(index));
        System.out.println("Entry Time: " + entryTimes.get(index).format(DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss")));
    }

    private static void generateDailyReport() {
        LocalDate today = LocalDate.now();
        double totalRevenue = 0;
        System.out.println("Daily Report for " + today.format(DateTimeFormatter.ofPattern("dd-MM-yyyy")));
        for (int i = 0; i < bills.size(); i++) {
            if (exitTimes.get(i).toLocalDate().equals(today)) {
                totalRevenue += bills.get(i);
            }
        }
        System.out.println("Total Revenue: ₹" + totalRevenue);
    }

    private static void generateMonthlyReport() {
        YearMonth currentMonth = YearMonth.now();
        double totalRevenue = 0;
        System.out.println("Monthly Report for " + currentMonth.format(DateTimeFormatter.ofPattern("MM-yyyy")));
        for (int i = 0; i < bills.size(); i++) {
            YearMonth exitMonth = YearMonth.from(exitTimes.get(i));
            if (exitMonth.equals(currentMonth)) {
                totalRevenue += bills.get(i);
            }
        }
        System.out.println("Total Revenue: ₹" + totalRevenue);
    }
}
