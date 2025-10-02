# EJERCICIO-DE-PROGRAMACI-N

#include <stdio.h>  

int main() {
    
    int id_producto;
    char nombre_producto[50];  
    int stock; 
    float precio; 
    int cantidad_a_vender; 
    
    int opcion; 
    
  
    printf("Vamos a registrar el producto:\n");
    printf("Ingresa el ID: ");
    scanf("%d", &id_producto); 
    
    printf("Ingresa el nombre: ");
    scanf("%s", &nombre_producto);  
    
    printf("Ingresa el stock inicial: ");
    scanf("%d", &stock);
    
    printf("Ingresa el precio unitario: "); 
    scanf("%f", &precio); 
    
    printf("¡Listo! Producto registrado: %s, stock %d, precio %.2f\n", nombre_producto, stock, precio); 
    
   
    while (1) {  
        printf("\nIngresa cantidad (o 0 para salir): ");
        scanf("%d", &cantidad_a_vender);
        
        if (cantidad_a_vender == 0) {
            printf("Listo!\n");
            break;  
        }
        
        if (cantidad_a_vender > stock) {
            printf("No hay suficiente stock. Solo hay %d.\n", stock);
        } else if (cantidad_a_vender < 0) {
            printf("Cantidad no puede ser negativa, tonto.\n");  
        } else {
            stock = stock - cantidad_a_vender;  
            float total = cantidad_a_vender * precio;
            printf("Vendiste %d unidades por %.2f total.\n", cantidad_a_vender, total);
            printf("Stock ahora: %d\n", stock);
        }
    }
    
    return 0;  // Fin del programa
}

