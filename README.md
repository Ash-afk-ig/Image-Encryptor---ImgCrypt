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
 
