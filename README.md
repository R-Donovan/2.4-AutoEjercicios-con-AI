,,,
Este es el codigo en C, el cual realiza una Tabla de multiplicacion
,,,

,,,
# 2.4-AutoEjercicios-con-AI

#include <iostream>

/**
* @brief Generates a multiplication table up to a specified number.
*
* This function generates a multiplication table from 1 to the specified number.
* The table is displayed in the console.
*
* @param n The number up to which the multiplication table should be generated.
*/
void generateMultiplicationTable(int n) {
    // Validate the input
    if (n <= 0) {
        std::cout << "Invalid input. The number should be greater than zero.\n";
        return;
    }

    // Generate the multiplication table
    std::cout << "Multiplication Table up to " << n << ":\n";
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {
            std::cout << i << " x " << j << " = " << (i * j) << "\t";
        }
        std::cout << "\n";
    }
}

int main() {
    int number;

    // Prompt the user for input
    std::cout << "Enter a number: ";
    std::cin >> number;
	    // Generate and display the multiplication table
    generateMultiplicationTable(number);
 
    return 0;
}
,,,

,,,
Este es el codigo de ensamblador
,,,

; Include necesario para la entrada y salida estándar
#include <iostream>

; Función que genera una tabla de multiplicación hasta un número especificado
; RDI: Parámetro 'n' (número hasta el cual se generará la tabla)
generateMultiplicationTable:
    ; Validar la entrada (n <= 0)
    cmp rdi, 0
    jle .Linvalid_input

    ; Imprimir encabezado de la tabla
    mov rdi, "Multiplication Table up to "
    mov rax, 1
    mov rsi, rdi
    mov rdx, 26
    syscall

    ; Iniciar el bucle externo (i)
    mov rsi, 1
    .Louter_loop:
        ; Iniciar el bucle interno (j)
        mov rdx, 1
        .Linner_loop:
            ; Imprimir i, " x ", j, " = ", (i * j), "\t"
            mov rax, 1
            mov rdi, rsi
            mov rsi, rdx
            mul rsi
            push rax
            mov rdi, rax
            mov rax, 1
            mov rsi, rdi
            mov rdx, 1
            mov rcx, 2
            mov rbx, 0
            syscall
            pop rax
            mov rax, rsi
            mov rsi, rdi
            mov rdi, rax
            mov rax, 1
            mov rdx, 9
            mov rcx, 1
            mov rbx, 0
            syscall

            ; Incrementar j
            inc rdx

            ; Comprobar si j <= n
            cmp rdx, [rbp - 4]
            jle .Linner_loop

            ; Salto de línea
            mov rdi, "\n"
            mov rax, 1
            mov rsi, rdi
            mov rdx, 1
            syscall

        ; Incrementar i
        inc rsi

        ; Comprobar si i <= n
        cmp rsi, [rbp - 4]
        jle .Louter_loop

    ; Retornar
    ret

.Linvalid_input:
    ; Imprimir mensaje de error
    mov rdi, "Invalid input. The number should be greater than zero.\n"
    mov rax, 1
    mov rsi, rdi
    mov rdx, 47
    syscall
    ret

; Función principal
main:
    ; Reservar espacio en la pila para la variable 'number'
    sub rsp, 8

    ; Prompt al usuario para la entrada
    mov rdi, "Enter a number: "
    mov rax, 1
    mov rdx, 19
    syscall

    ; Leer el número de la entrada estándar
    mov rdi, 0
    lea rsi, [rsp]
    mov rdx, 8
    mov rax, 0
    syscall

    ; Llamar a 'generateMultiplicationTable' con el número leído
    call generateMultiplicationTable

    ; Restaurar el puntero de la pila y retornar
    add rsp, 8
    ret






    // Generate and display the multiplication table
    generateMultiplicationTable(number);

    return 0;
}
