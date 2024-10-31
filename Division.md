import sympy as sp

# Definir la variable simbólica
x = sp.symbols('x')

# Definir las funciones
f = x**2
g = sp.exp(x)

# Calcular las integrales
integral_f = sp.integrate(f, (x, 0, 1))  # Integral de f(x) desde 0 hasta 1
integral_g = sp.integrate(g, (x, 1, 2))  # Integral de g(x) desde 1 hasta 2

# Calcular la división de las integrales
resultado = integral_f / integral_g

# Mostrar el resultado
resultado.evalf()  # evalf() da una aproximación numérica
