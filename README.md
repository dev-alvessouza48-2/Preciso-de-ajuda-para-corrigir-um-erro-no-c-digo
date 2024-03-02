# Estou com dificuldade de plotar o gráfico deste cálculo de otmização geométrica no python.

# Importar bibliotecas
import numpy as np
from scipy.optimize import minimize
import matplotlib.pyplot as plt

# Função para calcular a energia potencial da molécula H2
def energia_potencial(x):
  """
  Esta função calcula a energia potencial da molécula H2.

  Argumentos:
    x: Um vetor com um único elemento que representa a distância entre os átomos (bohr).

  Retorno:
    O valor escalar da energia potencial (hartree).
  """
  # Eu acredito que o erro deva estar aqui, já modifiquei os valores e nada.
  r = x[0]
  return 0.5 * k * (r - r_eq)**2

# Definir constantes
k = 4.5563e3 # constante de força da mola (hartree/bohr^2)
r_eq = 0.7414 # distância de equilíbrio entre os átomos (bohr)

# Definir parâmetros iniciais
x0 = np.array([0.8]) # chute inicial para a distância entre os átomos (bohr)

# Minimizar a energia potencial
resultado = minimize(energia_potencial, x0, method='Nelder-Mead')

# Extrair a energia potencial mínima
energia_minima = resultado.fun

# Importar Pylance
from pylance import pylance

# Analisar o código com Pylance
pylance.analyze(code=open(__file__).read())

# Imprimir os resultados
print("Distância otimizada (bohr):", resultado.x[0])
print("Energia potencial mínima (hartree):", energia_minima)

# Definir os dados para o gráfico
x = np.linspace(0.5, 1.5, 100)
y = energia_potencial(x)

# Criar a figura
fig, ax = plt.subplots()

# Plotar a curva de energia potencial
ax.plot(x, y, label="Energia Potencial")

# Adicionar rótulos aos eixos
ax.set_xlabel("Distância entre os átomos (bohr)")
ax.set_ylabel("Energia potencial (hartree)")

# Adicionar um marcador no mínimo
ax.scatter(resultado.x[0], energia_minima, marker="x", color="red", label="Mínimo")

# Adicionar legenda
ax.legend()

# Mostrar a figura
plt.show()
