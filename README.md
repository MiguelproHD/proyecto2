import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Scanner;

public class BancAmiga {

  private static final double MAX_WITHDRAWAL = 1000.0; // Monto maximo
  private static double balance = 1000.0; // Dinero inicial en bolivares

  private static final String CLIENTS_FOLDER = "clientes.in";
  private static final String CLIENTS_FILE = "clientes.txt";

  public static void main(String[] args) {
    File clientsFolder = new File(CLIENTS_FOLDER);
    if (!clientsFolder.exists()) {
      clientsFolder.mkdir();
    }

    try (Scanner scanner = new Scanner(System.in)) {
     
      System.out.print("Ingrese su nombre: ");
      String nombre = scanner.nextLine();

      System.out.print("Ingrese su nÃºmero de cÃ©dula: ");
      String id = scanner.nextLine();

      System.out.print("Ingrese su edad: ");
      int edad = scanner.nextInt();
      scanner.nextLine(); r

      String data = "Nombre: " + nombre + "\nCÃ©dula: " + id + "\nEdad: " + edad + "\n";
      File clientsFile = new File(CLIENTS_FOLDER, CLIENTS_FILE);
      try (FileWriter fileWriter = new FileWriter(clientsFile, true)) {
        fileWriter.write(data);
        System.out.println("Datos del cliente guardados exitosamente en " + clientsFile.getAbsolutePath());
      } catch (IOException e) {
        System.out.println("Error al guardar datos del cliente: " + e.getMessage());
      }
      System.out.println("\nBienvenido al Banco, " + nombre + "!");
      System.out.println("-----------------------------");

      int option;
      do {
        displayMenu();
        option = scanner.nextInt();
        scanner.nextLine(); 

        switch (option) {
          case 1:
            checkBalance();
            break;
          case 2:
            makeDeposit();
            break;
          case 3:
            makeWithdrawal();
            break;
          case 4:
            System.out.println("Saliendo del sistema...");
            break;
          default:
            System.out.println("OpciÃ³n no vÃ¡lida. Intente nuevamente.");
        }
      } while (option != 4);

      scanner.close();
    }
  }
  private static void displayMenu() {
    System.out.println("\nBienvenido al Banco Simulado");
    System.out.println("--------------------------");
    System.out.println("1. Consultar saldo");
    System.out.println("2. Realizar depÃ³sito");
    System.out.println("3. Realizar retiro");
    System.out.println("4. Salir");
    System.out.print("Ingrese una opciÃ³n: ");
  }
   private static void checkBalance() {
        System.out.println("Su saldo actual es: $" + balance);
    }
    private static void makeDeposit() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Ingrese la cantidad a depositar: ");
        double amount = scanner.nextDouble(); 
        scanner.nextLine(); 
        if (amount <= 0) {
            System.out.println("El monto del depÃ³sito debe ser un valor positivo.");
        } else {
            balance += amount;
            System.out.println("DepÃ³sito realizado con Ã©xito. Su nuevo saldo es: $" + balance);
            recordTransaction(amount, "DepÃ³sito");
        }
    }
    private static void makeWithdrawal() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Ingrese la cantidad a retirar: ");
        double amount = scanner.nextDouble(); 
      String nextLine = scanner.nextLine(); 
        if (amount <= 0) {
            System.out.println("El monto del retiro debe ser un valor positivo.");
        } else if (amount > balance) {
            System.out.println("Saldo insuficiente. Su saldo actual es: $" + balance);
        } else if (amount > MAX_WITHDRAWAL) {
            System.out.println("El monto del retiro excede el lÃ­mite mÃ¡ximo de $" + MAX_WITHDRAWAL + ".");
        } else {
            balance -= amount;
            System.out.println("Retiro realizado con Ã©xito. Su nuevo saldo es: $" + balance);
            recordTransaction(amount, "Retiro");
        }
    }

    private static void recordTransaction(double amount, String depÃ³sito) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }
    }


 

  
