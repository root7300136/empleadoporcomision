# empleadoporcomision
// Clase Empleado
public class Empleado {
  protected final String nombre;
  protected final String apellido;
  protected final String numeroSeguridadSocial;

  public Empleado(String nombre, String apellido, String numeroSeguridadSocial) {
    this.nombre = nombre;
    this.apellido = apellido;
    this.numeroSeguridadSocial = numeroSeguridadSocial;
  }

  public String getNombre() {
    return nombre;
  }

  public String getApellido() {
    return apellido;
  }

  public String getNumeroSeguridadSocial() {
    return numeroSeguridadSocial;
  }

  @Override
  public String toString() {
    return "Nombre: " + nombre + " " + apellido + "\n" +
           "Número de Seguridad Social: " + numeroSeguridadSocial;
  }
}

// Clase Empleado por Comisión que hereda de Empleado
public class EmpleadoPorComision extends Empleado {
  private double ventasBrutas;
  private double tasaComision;

  public EmpleadoPorComision(String nombre, String apellido, String numeroSeguridadSocial,
                             double ventasBrutas, double tasaComision) {
    super(nombre, apellido, numeroSeguridadSocial);
    if (ventasBrutas < 0.0)
      throw new IllegalArgumentException("Las ventas brutas deben ser >= 0.0");
    if (tasaComision <= 0.0 || tasaComision >= 1.0)
      throw new IllegalArgumentException("La tasa de comisión debe ser > 0.0 y < 1.0");
    this.ventasBrutas = ventasBrutas;
    this.tasaComision = tasaComision;
  }

  public void setVentasBrutas(double ventasBrutas) {
    if (ventasBrutas < 0.0)
      throw new IllegalArgumentException("Las ventas brutas deben ser >= 0.0");
    this.ventasBrutas = ventasBrutas;
  }

  public void setTasaComision(double tasaComision) {
    if (tasaComision <= 0.0 || tasaComision >= 1.0)
      throw new IllegalArgumentException("La tasa de comisión debe ser > 0.0 y < 1.0");
    this.tasaComision = tasaComision;
  }

  public double calcularEarnings() {
    return ventasBrutas + (tasaComision * ventasBrutas);
  }

  @Override
  public String toString() {
    return super.toString() + "\n" +
           "Earnings: " + calcularEarnings();
  }
}

// Clase Driver para probar la clase Empleado por Comisión
import java.util.Scanner;

public class Driver {
  public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);

    System.out.print("Ingrese el primer nombre del empleado: ");
    String nombre = scanner.nextLine();

    System.out.print("Ingrese el apellido del empleado: ");
    String apellido = scanner.nextLine();

    System.out.print("Ingrese el número de Seguridad Social del empleado: ");
    String numeroSeguridadSocial = scanner.nextLine();

    System.out.print("Ingrese las ventas brutas del empleado: ");
    double ventasBrutas = scanner.nextDouble();

    System.out.print("Ingrese la tasa de comisión del empleado (como decimal): ");
    double tasaComision = scanner.nextDouble();

    EmpleadoPorComision empleado = new Empleado
