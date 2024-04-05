# LogicaFuzzyIA


## Código de Implementação
```python
import numpy as np
import skfuzzy as fuzz
import matplotlib.pyplot as plt
from skfuzzy import control as ctrl

# Variáveis de entrada
conforto = ctrl.Antecedent(np.arange(0, 11, 1), 'conforto')
durabilidade = ctrl.Antecedent(np.arange(0, 11, 1), 'durabilidade')
preço = ctrl.Antecedent(np.arange(0, 11, 1), 'preço')

# Variável de saída
marca = ctrl.Consequent(np.arange(0, 11, 1), 'marca')

# Funções de pertinência
conforto.automf(3, names=['baixo', 'médio', 'alto'])
durabilidade.automf(3, names=['baixo', 'médio', 'alto'])
preço.automf(3, names=['baixo', 'médio', 'alto'])

marca['Olympikus'] = fuzz.trimf(marca.universe, [0, 0, 5])
marca['Nike'] = fuzz.trimf(marca.universe, [0, 5, 10])
marca['Adidas'] = fuzz.trimf(marca.universe, [5, 10, 15])

# Regras
regra1 = ctrl.Rule(conforto['médio'] & durabilidade['médio'] & preço['médio'], marca['Olympikus'])
regra2 = ctrl.Rule(conforto['alto'] & durabilidade['alto'] & preço['médio'], marca['Nike'])
regra3 = ctrl.Rule(conforto['alto'] & durabilidade['alto'] & preço['alto'], marca['Adidas'])
regra4 = ctrl.Rule(conforto['baixo'] & durabilidade['alto'] & preço['médio'], marca['Nike'])
regra5 = ctrl.Rule(conforto['médio'] & durabilidade['médio'] & preço['alto'], marca['Adidas'])
regra6 = ctrl.Rule(conforto['médio'] & durabilidade['baixo'] & preço['médio'], marca['Olympikus'])
regra7 = ctrl.Rule(conforto['médio'] & durabilidade['baixo'] & preço['alto'], marca['Nike'])
regra8 = ctrl.Rule(conforto['alto'] & durabilidade['alto'] & preço['médio'], marca['Adidas'])
regra9 = ctrl.Rule(conforto['alto'] & durabilidade['médio'] & preço['médio'], marca['Nike'])
regra10 = ctrl.Rule(conforto['baixo'] & durabilidade['médio'] & preço['alto'], marca['Olympikus'])
regra11 = ctrl.Rule(conforto['médio'] & durabilidade['alto'] & preço['médio'], marca['Olympikus'])
regra12 = ctrl.Rule(conforto['alto'] & durabilidade['alto'] & preço['alto'], marca['Nike'])
regra13 = ctrl.Rule(conforto['alto'] & durabilidade['médio'] & preço['médio'], marca['Nike'])
regra14 = ctrl.Rule(conforto['alto'] & durabilidade['médio'] & preço['alto'], marca['Nike'])
regra15 = ctrl.Rule(conforto['médio'] & durabilidade['baixo'] & preço['baixo'], marca['Olympikus'])
regra16 = ctrl.Rule(conforto['alto'] & durabilidade['médio'] & preço['alto'], marca['Adidas'])
regra17 = ctrl.Rule(conforto['baixo'] & durabilidade['médio'] & preço['médio'], marca['Nike'])
regra18 = ctrl.Rule(conforto['médio'] & durabilidade['alto'] & preço['baixo'], marca['Olympikus'])
regra19 = ctrl.Rule(conforto['alto'] & durabilidade['baixo'] & preço['alto'], marca['Adidas'])
regra20 = ctrl.Rule(conforto['médio'] & durabilidade['médio'] & preço['médio'], marca['Nike'])
regra21 = ctrl.Rule(conforto['médio'] & durabilidade['alto'] & preço['alto'], marca['Adidas'])
regra22 = ctrl.Rule(conforto['baixo'] & durabilidade['alto'] & preço['médio'], marca['Olympikus'])
regra23 = ctrl.Rule(conforto['médio'] & durabilidade['alto'] & preço['alto'], marca['Nike'])
regra24 = ctrl.Rule(conforto['alto'] & durabilidade['médio'] & preço['médio'], marca['Adidas'])
regra25 = ctrl.Rule(conforto['médio'] & durabilidade['médio'] & preço['alto'], marca['Olympikus'])
regra26 = ctrl.Rule(conforto['alto'] & durabilidade['alto'] & preço['baixo'], marca['Nike'])
regra27 = ctrl.Rule(conforto['baixo'] & durabilidade['médio'] & preço['alto'], marca['Adidas'])
regra28 = ctrl.Rule(conforto['médio'] & durabilidade['baixo'] & preço['médio'], marca['Olympikus'])
regra29 = ctrl.Rule(conforto['alto'] & durabilidade['médio'] & preço['baixo'], marca['Nike'])
regra30 = ctrl.Rule(conforto['baixo'] & durabilidade['médio'] & preço['baixo'], marca['Olympikus'])
regra31 = ctrl.Rule(conforto['baixo'] & durabilidade['baixo'] & preço['baixo'], marca['Olympikus'])
regra32 = ctrl.Rule(conforto['baixo'] & durabilidade['baixo'] & preço['baixo'], marca['Olympikus'])
regra33 = ctrl.Rule(conforto['baixo'] & durabilidade['baixo'] & preço['baixo'], marca['Nike'])

# Sistema de controle
sistema_marca = ctrl.ControlSystem([regra1, regra2, regra3, regra4, regra5, regra6, regra7, regra8, regra9, regra10, regra11, regra12, regra13, regra14, regra15, regra16, regra17, regra18, regra19, regra20, regra21, regra22, regra23, regra24, regra25, regra26, regra27, regra28, regra29, regra30, regra31, regra32, regra33])
marca_final = ctrl.ControlSystemSimulation(sistema_marca)

# Entrada do usuário
conforto_input = float(input("Digite uma pontuação de conforto (0 a 10): "))
durabilidade_input = float(input("Digite uma pontuação de durabilidade (0 a 10): "))
preço_input = float(input("Digite uma pontuação de preço (0 a 10): "))

# Computar a recomendação
marca_final.input['conforto'] = conforto_input
marca_final.input['durabilidade'] = durabilidade_input
marca_final.input['preço'] = preço_input
marca_final.compute()

# Mostrar o resultado
print("perfil do cliente:", marca_final.output['marca'])

# Plotar o gráfico de pertinência
marca.view(sim=marca_final)

plt.show()

```
