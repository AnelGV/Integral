# Integral
import sympy as sp

# Definir la variable y la función a integrar
x = sp.symbols('x')
funcion = sp.exp(3 * x)

# Resolver la integral
integral = sp.integrate(funcion, x)

# Mostrar el resultado
print(integral)
