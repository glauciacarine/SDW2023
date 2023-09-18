# SDW2023
Projeto SDW2023

import csv

def extrair_dados(arquivo_entrada):
    with open(arquivo_entrada, 'r') as arquivo_csv:
        leitor_csv = csv.DictReader(arquivo_csv)
        return list(leitor_csv)

def transformar_dados(dados):
    return sorted(dados, key=lambda x: float(x['Saldo']))

def carregar_dados(arquivo_saida, dados_transformados):
    with open(arquivo_saida, 'w', newline='') as arquivo_csv:
        colunas = ['UserID', 'Saldo']
        escritor_csv = csv.DictWriter(arquivo_csv, fieldnames=colunas)
        escritor_csv.writeheader()
        for linha in dados_transformados:
            escritor_csv.writerow(linha)

def etl(arquivo_entrada, arquivo_saida):
    # Extração
    dados_extraidos = extrair_dados(arquivo_entrada)
    
    # Transformação
    dados_transformados = transformar_dados(dados_extraidos)
    
    # Carga
    carregar_dados(arquivo_saida, dados_transformados)

if __name__ == "__main__":
    arquivo_entrada = 'dados.csv'
    arquivo_saida = 'dados_ordenados.csv'
    etl(arquivo_entrada, arquivo_saida)
    print(f"Ação ETL concluída. Dados transformados foram salvos em '{arquivo_saida}'.")
