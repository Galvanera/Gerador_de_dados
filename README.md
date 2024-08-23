Gerador de Dados de Compras Fictícias
Este repositório contém um script Python que gera dados fictícios de compras, incluindo nomes de clientes, valores de compras, formas de pagamento, datas e horários. Os dados são salvos em um arquivo Excel para fácil manipulação e análise.

Funcionalidades
Geração de Nomes Fictícios: Utiliza a biblioteca Faker para gerar nomes em português do Brasil.
Datas Aleatórias: Gera datas aleatórias dentro de um intervalo especificado.
Valores de Compras: Gera valores de compras aleatórios entre 10 e 1000.
Formas de Pagamento: Inclui várias formas de pagamento como cartão de crédito, débito, vale alimentação, vale refeição e dinheiro.
Exportação para Excel: Salva os dados gerados em um arquivo Excel (dados_compras.xlsx).
Como Usar
Instale as bibliotecas necessárias:
pip install pandas faker openpyxl

Clone este repositório:
git clone https://github.com/seu-usuario/gerador-dados-compras.git
cd gerador-dados-compras

Execute o script:
python gerar_dados_compras.py

Veja os dados gerados:
O script salvará os dados gerados em um arquivo Excel chamado dados_compras.xlsx.
Exemplo de Código
Python

import random
import pandas as pd
from faker import Faker
from datetime import datetime, timedelta

def generate_random_date():
    start_date = datetime(2024, 1, 1)
    end_date = datetime(2024, 5, 1)
    time_between_dates = end_date - start_date
    random_number_of_days = random.randrange(time_between_dates.days)
    random_date = start_date + timedelta(days=random_number_of_days)
    return random_date.strftime("%d/%m/%Y")

fake = Faker("pt_BR")
nomes = [fake.name() for _ in range(100)]

ids = []
valores = []
formas_pagamento = []
datas = []
horarios = []
nomes_clientes = []

for i in range(1, 1001):
    id_compra = i
    valor_compra = round(random.uniform(10, 1000), 2)
    forma_pagamento = random.choice(["Cartão de crédito", "Cartão Débito", "Vale Alimentação", "Vale Refeição", "Dinheiro"])
    data = generate_random_date()
    horario = f"{random.randint(0, 23):02d}:{random.randint(0, 59):02d}"
    nome_cliente = random.choice(nomes)
    ids.append(id_compra)
    valores.append(valor_compra)
    formas_pagamento.append(forma_pagamento)
    datas.append(data)
    horarios.append(horario)
    nomes_clientes.append(nome_cliente)

df = pd.DataFrame({
    "ID_compra": ids,
    "Valor": valores,
    "Forma de pagamento": formas_pagamento,
    "Data": datas,
    "Horário": horarios,
    "Nome do cliente": nomes_clientes
})

nome_arquivo = "dados_compras.xlsx"
df.to_excel(nome_arquivo, index=False)
print(f"Os dados foram salvos no arquivo {nome_arquivo}")
