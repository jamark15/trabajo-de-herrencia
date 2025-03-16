# trabajo-de-herrencia
es codigo en java se podra modificar
// CLASE BASE
/**
 * Representa un producto genérico con características básicas
 * @author TuNombre
 */
public class Producto {
    protected String nombre;
    protected double precio;

    /**
     * Constructor de la clase base
     * @param nombre Nombre del producto
     * @param precio Precio en dólares
     */
    public Producto(String nombre, double precio) {
        this.nombre = nombre;
        this.precio = precio;
    }

    /**
     * Muestra los detalles básicos del producto
     */
    public void mostrarDetalle() {
        System.out.println("Producto: " + nombre);
        System.out.println("Precio: $" + precio);
    }

    /**
     * Calcula el precio con impuesto básico
     * @return Precio con 10% de impuesto
     */
    public double calcularPrecioConImpuesto() {
        return precio * 1.10;
    }
}

// SUBCLASE 1
/**
 * Representa productos electrónicos con garantía extendida
 * extends Producto
 */
public class Electronico extends Producto {
    private int mesesGarantia;
    private String modelo;

    /**
     * Constructor de clase Electrónico
     * @param modelo Modelo específico del dispositivo
     * @param garantia Meses de garantía
     */
    public Electronico(String nombre, double precio, String modelo, int garantia) {
        super(nombre, precio); // Llama al constructor de Producto
        this.modelo = modelo;
        this.mesesGarantia = garantia;
    }

    @Override
    public void mostrarDetalle() {
        super.mostrarDetalle(); // Reutiliza el método de la clase base
        System.out.println("Modelo: " + modelo);
        System.out.println("Garantía: " + mesesGarantia + " meses");
    }

    /**
     * Método exclusivo para electrónicos
     * @return true si tiene garantía extendida
     */
    public boolean tieneGarantiaExtendida() {
        return mesesGarantia > 12;
    }
}

// SUBCLASE 2
/**
 * Representa productos alimenticios con fecha de caducidad
 * @extends Producto
 */
public class Alimento extends Producto {
    private String fechaCaducidad;

    public Alimento(String nombre, double precio, String fechaCaducidad) {
        super(nombre, precio);
        this.fechaCaducidad = fechaCaducidad;
    }

    @Override
    public void mostrarDetalle() {
        super.mostrarDetalle();
        System.out.println("Caduca: " + fechaCaducidad);
    }

    @Override
    public double calcularPrecioConImpuesto() {
        // Alimentos sin impuesto
        return precio;
    }
}

// CLASE PRINCIPAL
public class Main {
    public static void main(String[] args) {
        // Crear instancias
        Producto[] productos = {
                new Electronico("Smartphone", 799.99, "Xiaomi 12", 24),
                new Alimento("Leche Entera", 2.99, "2025-03-01"),
                new Producto("Libro", 19.99)
        };

        // Probar funcionalidades
        for (Producto p : productos) {
            p.mostrarDetalle();
            System.out.println("Precio final: $" + p.calcularPrecioConImpuesto());
            System.out.println("-------------------");

            // Método específico de Electrónico
            if (p instanceof Electronico) {
                Electronico e = (Electronico) p;
                System.out.println("Garantía extendida: " + e.tieneGarantiaExtendida());
            }
        }
    }
}

