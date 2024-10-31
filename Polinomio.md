import numpy as np

def multiplicar_polinomios(p1, p2):
    # Realiza la multiplicación de dos polinomios utilizando np.polymul
    resultado = np.polymul(p1, p2)
    return resultado

# Ejemplo de uso
# Polinomio 1: 3x^2 + 4x + 5
p1 = [3, 4, 5]

# Polinomio 2: 2x + 7
p2 = [2, 7]

# Multiplicación de los polinomios
resultado = multiplicar_polinomios(p1, p2)

# Mostrar el resultado
print("El resultado de la multiplicación de los polinomios es:", resultado)
