# college

 
B) Write C# program to make a class named Fruit with a data member to calculate 
the number of fruits in a basket. Create two other class named Apples and 
Mangoes to calculate the number of apples and mangoes in the basket. Display 
total number of fruits in the basket. 

using System; 
class Fruit 
{ 
protected static int totalFruits; 
public void DisplayTotalFruits() 
{ 
Console.WriteLine("Total number of fruits in the basket : " + totalFruits); 
} 
} 
class Apples : Fruit 
{ 
private int appleCount; 
public Apples(int apples) 
{ 
appleCount = apples; 
totalFruits += appleCount; 
} 
public void DisplayApples() 
{ 
Console.WriteLine("Number of apples in the basket : " + appleCount); 
} 
} 
class Mangoes : Fruit 
{ 
private int mangoCount; 
public Mangoes(int mangoes) 
{ 
mangoCount = mangoes; 
totalFruits += mangoCount; 
} 
public void DisplayMangoes() 
{ 
Console.WriteLine("Number of mangoes in the basket : " + mangoCount); 
} 
} 
namespace Myslip 
{ 
class Myslip
{ 
static void Main(string[] args) 
{ 
Apples a = new Apples(6); 
Mangoes m = new Mangoes(7); 
a.DisplayApples(); 
m.DisplayMangoes(); 
a.DisplayTotalFruits(); 
Console.ReadLine(); 
} 
} 
} 

*******************************************************************************************
java : 

1) Write a java program to display IPAddress and name of client machine.
Answer : 
import java.net.*;
public class IPTest
{
	public static void main(String args[])throws UnknownHostException
	{
		InetAddress addr=InetAddress.getLocalHost();
		String ipAddress=addr.getHostAddress();
		System.out.println("IP Address of localhost from Java Program:"+ ipAddress);
		String hostname=addr.getHostName();
		System.out.println("Name of hostname:"+hostname);
	}
}

*************************************************************************
2) Write a Java program to display sales details of Product (PID, PName, Qty, Rate, Amount) between two selected dates. (Assume Sales table is already created).
Answer : - 
import java.sql.*;
import java.util.Scanner;

public class SalesDetails {

    // Method to display sales details between two dates
    public static void displaySalesBetweenDates(Connection conn, String startDate, String endDate) {
        String query = "SELECT PID, PName, Qty, Rate, (Qty * Rate) AS Amount FROM Sales WHERE SaleDate BETWEEN ? AND ?";
        
        try (PreparedStatement stmt = conn.prepareStatement(query)) {
            // Set the date parameters
            stmt.setString(1, startDate);
            stmt.setString(2, endDate);

            ResultSet rs = stmt.executeQuery();

            // Print the header for the sales details
            System.out.println("PID | PName | Qty | Rate | Amount");
            System.out.println("----------------------------------");

            // Iterate through the result set and display sales details
            while (rs.next()) {
                int pid = rs.getInt("PID");
                String pname = rs.getString("PName");
                int qty = rs.getInt("Qty");
                double rate = rs.getDouble("Rate");
                double amount = rs.getDouble("Amount");

                System.out.println(pid + " | " + pname + " | " + qty + " | " + rate + " | " + amount);
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Database connection details
        String url = "jdbc:mysql://localhost:3307/productsalesdb";
        String user = "root";
        String password = ""; 


        // Get the start date and end date from the user
        System.out.print("Enter start date (YYYY-MM-DD): ");
        String startDate = scanner.nextLine();

        System.out.print("Enter end date (YYYY-MM-DD): ");
        String endDate = scanner.nextLine();

        // Establish the database connection
        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            System.out.println("\nSales details between " + startDate + " and " + endDate + ":");
            displaySalesBetweenDates(conn, startDate, endDate);
        } catch (SQLException e) {
            e.printStackTrace();
        }

        scanner.close();
    }
}


// i need to create database for this program : 
1: Open MySQL Command Line or MySQL Workbench and run:
-- Step 1: Create the database
CREATE DATABASE productsalesdb;

-- Step 2: Use the database
USE productsalesdb;

-- Step 3: Create the Sales table
CREATE TABLE Sales (
    PID INT,
    PName VARCHAR(100),
    Qty INT,
    Rate DOUBLE,
    SaleDate DATE
);

2:Insert Sample Data : 
INSERT INTO Sales (PID, PName, Qty, Rate, SaleDate) VALUES
(101, 'Laptop', 2, 45000.00, '2025-04-01'),
(102, 'Mouse', 5, 300.00, '2025-04-03'),
(103, 'Keyboard', 3, 800.00, '2025-04-05'),
(104, 'Monitor', 1, 12000.00, '2025-04-10'),
(105, 'Headphones', 4, 1500.00, '2025-04-15');

3: Update Connection in Java Program
String url = "jdbc:mysql://localhost:3307/productsalesdb";
String user = "root";
String password = ""; // or your MySQL root password

