# Sistema de Agenda

Programa em Python para gerenciar compromissos com persistência de dados.

## Estrutura do Código

### Programa Principal (agenda.py)

```python
import agenda_modulo

print("Programa de agenda".center(40, "="))
info = agenda_modulo.carregar_info()

if info:
    print("Seus compromissos salvos na agenda são:\n")
    for data, compromisso in info.items():
        print(f"{data} -> {compromisso}")
else:
    print("Nenhum compromisso salvo ainda!")

while True:
     escolha = input("\nAperte 0 para sair. Aperte qualquer outro botão para salvar um compromisso.")
     
     if escolha == "0":
          break
     else:
          data_agend = input("\nDigite a data do seu compromisso (Dia/Mês/Ano): ")
          compro_agend = input("Digite o seu compromisso:")
          
          agenda_modulo.salvar_info(data_agend, compro_agend)
          print(f"\nCompromisso para o dia {data_agend} foi salvo com sucesso!")
          
          print("Obrigado por usar o programa! ".center(45, "="))
```
### Modulo de Gerenciamento


```python

import json
import os

ARQUIVO_AGENDA = "agenda.json"

def carregar_info():
    if os.path.exists(ARQUIVO_AGENDA):
        with open(ARQUIVO_AGENDA, 'r', encoding='utf-8') as f:
            return json.load(f)
    return {}

def salvar_info(data, compromisso):
    dados = carregar_info()
    dados[data] = compromisso
    with open(ARQUIVO_AGENDA, 'w', encoding='utf-8') as f:
        json.dump(dados, f, ensure_ascii=False, indent=2)
```

#### Funcionamento
O programa carrega compromissos salvos anteriormente

* Exibe todos os compromissos existentes

* Usuário escolhe entre sair (0) ou adicionar novo compromisso

* Para adicionar, informa data e descrição

* O compromisso é salvo no arquivo agenda.json

```shell
python agenda.py
```


  
