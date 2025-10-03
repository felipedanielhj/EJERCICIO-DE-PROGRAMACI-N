# EJERCICIO-DE-PROGRAMACI-N

#include <stdio.h>

int main() {
    int id_producto;
    char nombre_producto[50];
    int stock;
    float precio;
    int cantidad_a_vender;
    int opcion;
    float ganancias = 0.0;   

    
    printf("Vamos a registrar el producto:\n");
    printf("Ingresa el ID: ");
    scanf("%d", &id_producto);

    printf("Ingresa el nombre: ");
    scanf("%s", nombre_producto);

    printf("Ingresa el stock inicial: ");
    scanf("%d", &stock);

    printf("Ingresa el precio unitario: ");
    scanf("%f", &precio);

    printf("¡Listo! Producto registrado: %s, stock %d, precio %.2f\n", 
            nombre_producto, stock, precio);

    while (1) {
        printf("\n--- MENÚ ---\n");
        printf("1. Vender producto\n");
        printf("2. Reabastecer producto\n");
        printf("3. Consultar información del producto\n");
        printf("4. Ver ganancias obtenidas\n");
        printf("5. Salir\n");
        printf("Elige una opción: ");
        scanf("%d", &opcion);

        switch (opcion) {

            case 1: { 
                while (1) {
                    printf("\n¿Quieres vender? Ingresa cantidad (o 0 para volver al menú): ");
                    scanf("%d", &cantidad_a_vender);

                    if (cantidad_a_vender == 0) {
                        break;
                    }

                    if (cantidad_a_vender > stock) {
                        printf("No hay suficiente stock. Solo hay %d.\n", stock);
                    } else if (cantidad_a_vender < 0) {
                        printf("Cantidad no puede ser negativa.\n");
                    } else {
                        stock -= cantidad_a_vender;
                        float total = cantidad_a_vender * precio;
                        ganancias += total;
                        printf("Vendiste %d unidades por %.2f total.\n", cantidad_a_vender, total);
                        printf("Stock ahora: %d\n", stock);
                    }
                }
                break;
            }

            case 2: { 
                int cantidad_reabastecer;
                printf("¿Cuántas unidades deseas agregar al stock?: ");
                scanf("%d", &cantidad_reabastecer);

                if (cantidad_reabastecer > 0) {
                    stock += cantidad_reabastecer;
                    printf("Stock actualizado. Ahora tienes %d unidades.\n", stock);
                } else {
                    printf("Cantidad inválida.\n");
                }
                break;
            }

            case 3: { 
                printf("\n--- INFORMACIÓN DEL PRODUCTO ---\n");
                printf("ID: %d\n", id_producto);
                printf("Nombre: %s\n", nombre_producto);
                printf("Precio unitario: %.2f\n", precio);
                printf("Stock actual: %d\n", stock);
                printf("Ganancias acumuladas: %.2f\n", ganancias);
                break;
            }

            case 4: { 
                printf("\nGanancias totales hasta ahora: %.2f\n", ganancias);
                break;
            }

            case 5: { 
                printf("Gracias por usar el programa.\n");
                return 0;
            }

            default:
                printf("Opción inválida. Intenta otra vez.\n");
                break;
        }
    }

    return 0;
}

