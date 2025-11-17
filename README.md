#include <stdio.h>
#include <stdlib.h>

#define MAX_PRODUCTOS 5
#define MAX_NOMBRE 50

char nombres[MAX_PRODUCTOS][MAX_NOMBRE];
int cantidades[MAX_PRODUCTOS];
float tiempos[MAX_PRODUCTOS];
float recursos[MAX_PRODUCTOS];

char (*ptrNombres)[MAX_NOMBRE] = nombres;
int *ptrCantidades = cantidades;
float *ptrTiempos = tiempos;
float *ptrRecursos = recursos;

float limiteTiempo, limiteRecursos;

int compararCadenas(char *str1, char *str2) {
    int i = 0;
    while (str1[i] != '\0' && str2[i] != '\0') {
        if (str1[i] != str2[i]) {
            return 0;
        }
        i++;
    }
    return (str1[i] == '\0' && str2[i] == '\0');
}

int buscarProducto(char *nombreBuscado) {
    for (int i = 0; i < MAX_PRODUCTOS; i++) {
        if (compararCadenas(ptrNombres[i], nombreBuscado)) {
            return i;
        }
    }
    return -1;
}

void ingresarProducto() {
    int indice = -1;
    for (int i = 0; i < MAX_PRODUCTOS; i++) {
        if (ptrNombres[i][0] == '\0') {
            indice = i;
            break;
        }
    }
    if (indice == -1) {
        printf("No hay espacio para más productos.\n");
        return;
    }
    printf("Ingrese nombre del producto: ");
    scanf("%s", ptrNombres[indice]);
    printf("Ingrese cantidad demandada: ");
    scanf("%d", &ptrCantidades[indice]);
    printf("Ingrese tiempo de fabricación por unidad: ");
    scanf("%f", &ptrTiempos[indice]);
    printf("Ingrese recursos por unidad: ");
    scanf("%f", &ptrRecursos[indice]);
    printf("Producto ingresado exitosamente.\n");
}

void editarProducto() {
    char nombreBuscado[MAX_NOMBRE];
    printf("Ingrese nombre del producto a editar: ");
    scanf("%s", nombreBuscado);
    int indice = buscarProducto(nombreBuscado);
    if (indice == -1) {
        printf("Producto no encontrado.\n");
        return;
    }
    printf("Producto encontrado. Ingrese nuevos datos:\n");
    printf("Nueva cantidad: ");
    scanf("%d", &ptrCantidades[indice]);
    printf("Nuevo tiempo por unidad: ");
    scanf("%f", &ptrTiempos[indice]);
    printf("Nuevos recursos por unidad: ");
    scanf("%f", &ptrRecursos[indice]);
    printf("Producto editado exitosamente.\n");
}

void eliminarProducto() {
    char nombreBuscado[MAX_NOMBRE];
    printf("Ingrese nombre del producto a eliminar: ");
    scanf("%s", nombreBuscado);
    int indice = buscarProducto(nombreBuscado);
    if (indice == -1) {
        printf("Producto no encontrado.\n");
        return;
    }
    for (int i = indice; i < MAX_PRODUCTOS - 1; i++) {
        int j = 0;
        while (ptrNombres[i+1][j] != '\0') {
            ptrNombres[i][j] = ptrNombres[i+1][j];
            j++;
        }
        ptrNombres[i][j] = '\0';
        ptrCantidades[i] = ptrCantidades[i+1];
        ptrTiempos[i] = ptrTiempos[i+1];
        ptrRecursos[i] = ptrRecursos[i+1];
    }
    ptrNombres[MAX_PRODUCTOS-1][0] = '\0';
    ptrCantidades[MAX_PRODUCTOS-1] = 0;
    ptrTiempos[MAX_PRODUCTOS-1] = 0.0;
    ptrRecursos[MAX_PRODUCTOS-1] = 0.0;
    printf("Producto eliminado exitosamente.\n");
}

void calcularYVerificar() {
    float tiempoTotal = 0.0, recursoTotal = 0.0;
    for (int i = 0; i < MAX_PRODUCTOS; i++) {
        if (ptrNombres[i][0] != '\0') {
            tiempoTotal += ptrCantidades[i] * ptrTiempos[i];
            recursoTotal += ptrCantidades[i] * ptrRecursos[i];
        }
    }
    printf("Tiempo total requerido: %.2f\n", tiempoTotal);
    printf("Recursos totales requeridos: %.2f\n", recursoTotal);
    int puedeCumplir = (tiempoTotal <= limiteTiempo && recursoTotal <= limiteRecursos);
    printf("¿Puede cumplirse la demanda? %s\n", puedeCumplir ? "Sí" : "No");
}

int main() {
    for (int i = 0; i < MAX_PRODUCTOS; i++) {
        nombres[i][0] = '\0';
        cantidades[i] = 0;
        tiempos[i] = 0.0;
        recursos[i] = 0.0;
    }
    printf("Ingrese límite de tiempo disponible: ");
    scanf("%f", &limiteTiempo);
    printf("Ingrese límite de recursos disponible: ");
    scanf("%f", &limiteRecursos);

    int opcion;
    while (1) {
        printf("\n--- Menú ---\n");
        printf("1. Ingresar producto\n");
        printf("2. Editar producto\n");
        printf("3. Eliminar producto\n");
        printf("4. Calcular y verificar demanda\n");
        printf("5. Salir\n");
        printf("Seleccione opción: ");
        scanf("%d", &opcion);
        switch (opcion) {
            case 1:
                ingresarProducto();
                break;
            case 2:
                editarProducto();
                break;
            case 3:
                eliminarProducto();
                break;
            case 4:
                calcularYVerificar();
                break;
            case 5:
                printf("Saliendo del programa.\n");
                return 0;
            default:
                printf("Opción inválida.\n");
        }
    }
    return 0;
}

