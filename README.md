11 i) 
 
import java.util.*; 
 
public class MaxProductSubarray { 
    public static void main(String[] args) { 
        Scanner sc = new Scanner(System.in); 
         
        if (sc.hasNextLine()) { 
            String line = sc.nextLine(); 
            try { 
                String[] parts = line.trim().split("\\s+"); 
                double[] nums = new double[parts.length]; 
                for (int i = 0; i < parts.length; i++) { 
                    nums[i] = Double.parseDouble(parts[i]); 
                } 
 
                double max = nums[0], min = nums[0], res = nums[0]; 
                for (int i = 1; i < nums.length; i++) { 
                    double n = nums[i]; 
                    double temp = Math.max(n, Math.max(max * n, min * n)); 
                    min = Math.min(n, Math.min(max * n, min * n)); 
                    max = temp; 
                    res = Math.max(res, max); 
                } 
 
                System.out.printf("%.2f\n", res); 
            } catch (NumberFormatException e) {  
                System.out.println("Invalid Input"); 
            } 
        } else { 
            System.out.println("No input provided.");  
        } 
        sc.close();  
    } 
} 
 
 
 
14. i) 
import java.util.*; 
 
public class CloseStrings { 
    public static void main(String[] args) { 
        Scanner sc = new Scanner(System.in); 
 
        if (!sc.hasNextLine()) { 
            System.out.println("Invalid Input"); 
            return; 
        } 
        String s1 = sc.nextLine(); 
 
        if (!sc.hasNextLine()) { 
            System.out.println("Invalid Input"); 
            return; 
        } 
        String s2 = sc.nextLine(); 
 
        if (s1.length() != s2.length()) { 
            System.out.println("false"); 
            return; 
        } 
 
        int[] a = new int[26], b = new int[26]; 
        for (char c : s1.toCharArray()) a[c - 'A']++; 
        for (char c : s2.toCharArray()) b[c - 'A']++; 
 
        for (int i = 0; i < 26; i++) { 
            if ((a[i] > 0) != (b[i] > 0)) { 
                System.out.println("false"); 
                return; 
            } 
        } 
 
        List<Integer> l1 = new ArrayList<>(), l2 = new ArrayList<>(); 
        for (int i = 0; i < 26; i++) { 
            if (a[i] > 0) l1.add(a[i]); 
            if (b[i] > 0) l2.add(b[i]); 
        } 
 
        Collections.sort(l1); 
        Collections.sort(l2); 
        System.out.println(l1.equals(l2)); 
    } 
} 
 
 
 
 
 
16   .i) 
import java.util.*; 
 
class Bank { 
    private double balance; 
    public Bank(double bal) { balance = bal; } 
 
    public synchronized void deposit(double amt) { balance += amt; } 
    public synchronized void withdraw(double amt) { 
        if (amt <= balance) balance -= amt; 
    } 
    public double getBalance() { return balance; } 
} 
 
class Task implements Runnable { 
    Bank acc; 
    Task(Bank acc) { this.acc = acc; } 
    public void run() { 
        acc.deposit(500); 
        acc.withdraw(200); 
    } 
} 
 
public class Main { 
    public static void main(String[] args) throws InterruptedException { 
        Bank acc1 = new Bank(1000); 
        Thread t1 = new Thread(new Task(acc1)); 
        Thread t2 = new Thread(new Task(acc1)); 
        t1.start(); t2.start(); 
        t1.join(); t2.join(); 
        System.out.println("Final: " + acc1.getBalance()); 
    } 
} 




















17)i)
import java.util.Scanner;

class Bike {
private String brand;
private String model;
private int year;
private float mileage;
private float rentalPrice;

// Constructor
public Bike(String brand, String model, int year, float mileage, float rentalPrice) {
if (year <= 1885 || mileage < 0 || rentalPrice <= 0) {
throw new IllegalArgumentException("Invalid input");
}
this.brand = brand;
this.model = model;
this.year = year;
this.mileage = mileage;
this.rentalPrice = rentalPrice;
}

// Method to calculate rental cost for a given number of days
public float calculateRentalCost(int days) {
return rentalPrice * days;
}

// Method to display bike details and rental cost
public void displayDetails(int days) {
System.out.printf("Brand: %s, Model: %s, Year: %d, Mileage: %.2f km/l, Rental Price: ₹%.2f%n",
brand, model, year, mileage, rentalPrice);
System.out.printf("Rental Cost for %d days: ₹%.2f%n", days, calculateRentalCost(days));
}
}

public class BikeRentalSystem {
public static void main(String[] args) {
Scanner sc = new Scanner(System.in);
try {
int N = Integer.parseInt(sc.nextLine());
if (N <= 0) {
throw new IllegalArgumentException("Invalid input");
}

Bike[] bikes = new Bike[N];
for (int i = 0; i < N; i++) {
String[] input = sc.nextLine().split(" ");
if (input.length != 5) {
throw new IllegalArgumentException("Invalid input");
}
String brand = input[0];
String model = input[1];
int year = Integer.parseInt(input[2]);
float mileage = Float.parseFloat(input[3]);
float rentalPrice = Float.parseFloat(input[4]);

bikes[i] = new Bike(brand, model, year, mileage, rentalPrice);
}

System.out.println("Bike Details:");
for (Bike bike : bikes) {
bike.displayDetails(5);
}
} catch (IllegalArgumentException e) {
System.out.println(e.getMessage());
} catch (Exception e) {
System.out.println("Invalid input");
}
}
}
17) ii)
import java.util.Scanner;

class ShoppingCart {
// Method to handle integer price
double calculateTotal(int price) {
return price;
}

// Method to handle double price
double calculateTotal(double price) {
return price;
}

// Method to handle string price
double calculateTotal(String price) {
try {
return Double.parseDouble(price);
} catch (NumberFormatException e) {
throw new IllegalArgumentException("Invalid input");
}
}
}

public class ShoppingCartTotal {
public static void main(String[] args) {
Scanner sc = new Scanner(System.in);
ShoppingCart cart = new ShoppingCart();
double total = 0;

try {
for (int i = 0; i < 3; i++) {
String input = sc.nextLine();
if (input.matches("\\d+")) { // Integer format
total += cart.calculateTotal(Integer.parseInt(input));
} else if (input.matches("\\d+\\.\\d+")) { // Floating-point format
total += cart.calculateTotal(Double.parseDouble(input));
} else { // String format
total += cart.calculateTotal(input);
}
}
System.out.printf("Total Cost: %.2f%n", total);
} catch (IllegalArgumentException e) {
System.out.println("Invalid input");
}
}
}
19) i)
import java.util.Scanner;

abstract class Vehicle {
abstract double fuelEfficiency(double fuel, double distance);
}

class Car extends Vehicle {
@Override
double fuelEfficiency(double fuel, double distance) {
return distance / fuel;
}
}

class Bike extends Vehicle {
@Override
double fuelEfficiency(double fuel, double distance) {
return distance / fuel;
}
}

public class VehicleManagementSystem {
public static void main(String[] args) {
Scanner sc = new Scanner(System.in);

String vehicleType = sc.nextLine();
double fuel = sc.nextDouble();
double distance = sc.nextDouble();

if (fuel <= 0 || distance <= 0) {
System.out.println("Invalid Input");
return;
}

Vehicle vehicle;

switch (vehicleType) {
case "Car":
vehicle = new Car();
break;
case "Bike":
vehicle = new Bike();
break;
default:
System.out.println("Invalid Vehicle Type");
return;
}

double efficiency = vehicle.fuelEfficiency(fuel, distance);
System.out.printf("%s Fuel Efficiency: %.2f km per liter.%n", vehicleType, efficiency);
}
}
19) ii)
import java.util.Scanner;

class Product {
double price;
String category;

Product(double price, String category) {
this.price = price;
this.category = category;
}

public double calculateFinalPrice() {
return price; // Base class does not apply any calculation.
}
}

class Electronics extends Product {
Electronics(double price) {
super(price, "Electronics");
}

@Override
public double calculateFinalPrice() {
if (price > 5000) {
price -= 500; // Apply ₹500 discount
}
price += price * 0.18; // Apply 18% GST
return price;
}
}

class Clothing extends Product {
Clothing(double price) {
super(price, "Clothing");
}

@Override
public double calculateFinalPrice() {
if (price > 2000) {
price -= 100; // Apply ₹100 discount
}
price += price * 0.05; // Apply 5% GST
return price;
}
}

class Grocery extends Product {
Grocery(double price) {
super(price, "Grocery");
}

@Override
public double calculateFinalPrice() {
if (price >= 5000) {
price -= price * 0.10; // Apply 10% bulk discount
}
return price; // No GST for grocery
}
}

public class ShoppingCart {
public static void main(String[] args) {
Scanner sc = new Scanner(System.in);

String category = sc.nextLine();
double price = sc.nextDouble();

if (price <= 0) {
System.out.println("Invalid Input");
return;
}

Product product;

switch (category) {
case "Electronics":
product = new Electronics(price);
break;
case "Clothing":
product = new Clothing(price);
break;
case "Grocery":
product = new Grocery(price);
break;
default:
System.out.println("Invalid Product Category");
return;
}

double finalPrice = product.calculateFinalPrice();
System.out.printf("Final Price: ₹%.2f%n", finalPrice);
}
}
 
