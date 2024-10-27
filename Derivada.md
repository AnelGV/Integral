import sympy as sp

def calcular_derivada(funcion, variable):
    # Definir la variable simbólica
    var = sp.symbols(variable)
    
    # Convertir la función a una expresión simbólica
    expr = sp.sympify(funcion)
    
    # Calcular la derivada
    derivada = sp.diff(expr, var)
    
    return derivada

# Ejemplo de uso
funcion = "x**3 + 2*x**2 + 5*x + 7"
variable = "x"

resultado = calcular_derivada(funcion, variable)
print(f"La derivada de {funcion} respecto a {variable} es: {resultado}")
