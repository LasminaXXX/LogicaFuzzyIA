# LogicaFuzzyIA


## Código de Implementação
```python
#importação das bibliotecas usadas no projeto
import numpy as np
import skfuzzy as fuzz
import matplotlib.pyplot as plt
from skfuzzy import control as ctrl

# Variáveis de entrada
conforto = ctrl.Antecedent(np.arange(0, 21, 1), 'conforto')
durabilidade = ctrl.Antecedent(np.arange(0, 21, 1), 'durabilidade')
preço = ctrl.Antecedent(np.arange(0, 21, 1), 'preço')
necessidade = ctrl.Antecedent(np.arange(0, 3, 1), 'necessidade')


# Variável de saída
marca = ctrl.Consequent(np.arange(0, 21, 1), 'marca')

# Funções de pertinência
conforto.automf(3, names=['baixo', 'médio', 'alto'])
durabilidade.automf(3, names=['baixo', 'médio', 'alto'])
preço.automf(3, names=['baixo', 'médio', 'alto'])
necessidade.automf(3, names=['esporte', 'casual', 'streetware'])

marca['Converse'] = fuzz.trimf(marca.universe, [0, 0, 5])
marca['Olympikus'] = fuzz.trimf(marca.universe, [0, 5, 10])
marca['Nike'] = fuzz.trimf(marca.universe, [5, 10, 15])
marca['Adidas'] = fuzz.trimf(marca.universe, [10, 15, 20])

# Regras
regra1 = ctrl.Rule(conforto['baixo'] | durabilidade['baixo'] | preço['alto'] | necessidade['casual'], marca['Converse'])
regra2 = ctrl.Rule(conforto['médio'] & durabilidade['médio'] & preço['médio'] & necessidade['esporte'], marca['Olympikus'])
regra3 = ctrl.Rule(conforto['alto'] & durabilidade['alto'] & preço['médio'] & necessidade['casual'], marca['Nike'])
regra4 = ctrl.Rule(conforto['alto'] & durabilidade['alto'] & preço['alto'] & necessidade['casual'], marca['Adidas'])
regra5 = ctrl.Rule(conforto['baixo'] & durabilidade['alto'] & preço['médio'] & necessidade['streetware'], marca['Nike'])
regra6 = ctrl.Rule(conforto['médio'] & durabilidade['médio'] & preço['alto'] & necessidade['streetware'], marca['Adidas'])
regra7 = ctrl.Rule(conforto['médio'] & durabilidade['baixo'] & preço['médio'] & necessidade['esporte'], marca['Olympikus'])
regra8 = ctrl.Rule(conforto['médio'] & durabilidade['baixo'] & preço['alto'] & necessidade['casual'], marca['Nike'])
regra9 = ctrl.Rule(conforto['alto'] & durabilidade['alto'] & preço['médio'] & necessidade['streetware'], marca['Adidas'])
regra10 = ctrl.Rule(conforto['alto'] & durabilidade['médio'] & preço['médio'] & necessidade['esporte'], marca['Nike'])
regra11 = ctrl.Rule(conforto['baixo'] & durabilidade['médio'] & preço['alto'] & necessidade['esporte'], marca['Olympikus'])
regra12 = ctrl.Rule(conforto['médio'] & durabilidade['alto'] & preço['baixo'] & necessidade['casual'], marca['Converse'])
regra13 = ctrl.Rule(conforto['alto'] & durabilidade['baixo'] & preço['médio'] & necessidade['streetware'], marca['Nike'])
regra14 = ctrl.Rule(conforto['médio'] & durabilidade['alto'] & preço['médio'] & necessidade['esporte'], marca['Olympikus'])
regra15 = ctrl.Rule(conforto['alto'] & durabilidade['alto'] & preço['alto'] & necessidade['esporte'], marca['Nike'])
regra16 = ctrl.Rule(conforto['médio'] & durabilidade['baixo'] & preço['baixo'] & necessidade['casual'], marca['Converse'])
regra17 = ctrl.Rule(conforto['alto'] & durabilidade['médio'] & preço['médio'] & necessidade['streetware'], marca['Nike'])


# Sistema de controle
sistema_marca = ctrl.ControlSystem([regra1, regra2, regra3, regra4, regra5, regra6, regra7, regra8, regra9, regra10, regra11, regra12, regra13, regra14, regra15, regra16, regra17])
marca_final = ctrl.ControlSystemSimulation(sistema_marca)

# Entrada do usuário
conforto_input = float(input("Digite uma pontuação de conforto (0 a 20): "))
durabilidade_input = float(input("Digite uma pontuação de durabilidade (0 a 20): "))
preço_input = float(input("Digite uma pontuação de preço (0 a 20): "))
necessidade_input = float(input("1- Esport\n2 - casual \n3 - moderno\nDigite um valor de acordo com sua necessidade: "))

# Computar a recomendação
marca_final.input['conforto'] = conforto_input
marca_final.input['durabilidade'] = durabilidade_input
marca_final.input['preço'] = preço_input
marca_final.input['necessidade'] = necessidade_input
marca_final.compute()

# Mostrar o resultado
print("Perfil do Cliente:", marca_final.output['marca'])

# Plotar o gráfico de pertinência
marca.view(sim=marca_final)

plt.show()

```
