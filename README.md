🚗 Parking Management System
A Java-based console application that efficiently manages parking spaces, vehicle entries, and billing. This system ensures seamless parking operations by allowing vehicle registration, automated billing, and report generation.

📌 Features
✅ Vehicle Registration – Add vehicle details (number, type, model, owner).
✅ Automated Billing – Calculates parking fees based on time, vehicle type, and peak hours.
✅ Search Functionality – Search vehicles by number, owner name, or entry time.
✅ Case-Insensitive Search – Ensures flexible lookup for vehicle details.
✅ Parking Fee Exemption – 1-hour free parking for all vehicle types.
✅ Report Generation – View daily and monthly revenue reports.

🛠️ Tech Stack
Language: Java
IDE: IntelliJ IDEA
Database: No database (currently operates in-memory using collections)

📂 Folder Structure
📦 ParkingManagementSystem  
 ┣ 📜 src/  
 ┃ ┣ 📜 Main.java         # Entry point of the application  
 ┃ ┣ 📜 Vehicle.java      # Vehicle class with details (number, type, model, owner)  
 ┃ ┣ 📜 ParkingLot.java   # Manages vehicle parking and billing  
 ┃ ┗ 📜 ReportGenerator.java # Handles report generation  
 ┣ 📜 .gitignore  
 ┣ 📜 README.md  
 ┗ 📜 LICENSE
 
🚀 Installation & Usage
1️⃣ Clone the Repository
git clone https://github.com/anandparayil/ParkingManagementSystem.git
cd ParkingManagementSystem

2️⃣ Run the Application
Open the project in IntelliJ IDEA.
Run Main.java.

3️⃣ Sample Input & Output
Register a Vehicle:
Enter vehicle details:  
Number: TN-10-AB-1234  
Type: Car  
Model: Honda City  
Owner: John Doe  
Vehicle added successfully! ✅  
Calculate Parking Fee:
Enter exit time: 3 hours  
Total Fee: ₹50  

📜 License
This project is licensed under the MIT License.
