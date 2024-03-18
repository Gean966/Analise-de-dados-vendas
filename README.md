import pandas as pd

def mostrar_dados():
    try:
        # Ler todas as linhas do arquivo Excel
        df = pd.read_excel(r"C:\Users\geana\Downloads\Base Vendas - 2022.xlsx")
        
        # Exibir todos os dados no console
        for index, row in df.iterrows():
            print(row)
        
    except Exception as e:
        print("Ocorreu um erro ao ler o arquivo:", e)

# Chamar a função para mostrar os dados
mostrar_dados()

import pandas as pd

def filtrar_e_exibir():
    try:
        # Ler o arquivo Excel
        df = pd.read_excel(r"C:\Users\geana\Downloads\Base Vendas - 2022.xlsx")
        
        # Converter a coluna 'Data da Venda' para o tipo datetime
        df['Data da Venda'] = pd.to_datetime(df['Data da Venda'])
        
        # Filtrar as datas da venda apenas para o período de 2022
        vendas_2022 = df[df['Data da Venda'].dt.year == 2022]
        
        # Exibir todas as informações das vendas do período de 2022 em uma tabela
        print(vendas_2022.to_string(index=False))
        
    except Exception as e:
        print("Ocorreu um erro ao ler o arquivo:", e)

# Chamar a função para filtrar e exibir as vendas do período de 2022
filtrar_e_exibir()



import pandas as pd
import matplotlib.pyplot as plt

def plotar_grafico():
    try:
        # Ler o arquivo Excel
        df = pd.read_excel(r"C:\Users\geana\Downloads\Base Vendas - 2022.xlsx")
        
        # Filtrar as transações do ano de 2022
        vendas_2022 = df[df['Data da Venda'].dt.year == 2022]
        
        # Contar a quantidade de transações para cada quantidade vendida em 2022
        vendas_1 = vendas_2022[vendas_2022['Qtd Vendida'] == 1].shape[0]
        vendas_2 = vendas_2022[vendas_2022['Qtd Vendida'] == 2].shape[0]
        vendas_3 = vendas_2022[vendas_2022['Qtd Vendida'] == 3].shape[0]
        
        # Plotar o gráfico de barras
        plt.figure(figsize=(8, 6))
        plt.bar(['1', '2', '3'], [vendas_1, vendas_2, vendas_3], color=['red', 'blue', 'green'])
        
        # Configurações do gráfico
        plt.title('Quantidade de Vendas por Quantidade Vendida em 2022')
        plt.xlabel('Quantidade Vendida')
        plt.ylabel('Número de Vendas')
        plt.grid(axis='y')
        
        # Exibir o gráfico
        plt.show()
        
    except Exception as e:
        print("Ocorreu um erro ao ler o arquivo:", e)

# Chamar a função para plotar o gráfico
plotar_grafico()


import pandas as pd

def filtrar_e_exibir():
    try:
        # Ler o arquivo Excel
        df = pd.read_excel(r"C:\Users\geana\Downloads\Base Vendas - 2022.xlsx")
        
        # Filtrar as transações com quantidade vendida maior ou igual a três
        vendas_maiores_ou_igual_3 = df[df['Qtd Vendida'] >= 3]
        
        # Exibir todas as informações das vendas com quantidade vendida maior ou igual a três em uma tabela
        print(vendas_maiores_ou_igual_3)
        
    except Exception as e:
        print("Ocorreu um erro ao ler o arquivo:", e)

# Chamar a função para filtrar e exibir as vendas com quantidade vendida maior ou igual a três
filtrar_e_exibir()


import pandas as pd

def tabela_transacoes_por_id_loja():
    try:
        # Ler o arquivo Excel
        df = pd.read_excel(r"C:\Users\geana\Downloads\Base Vendas - 2022.xlsx")
        
        # Agrupar as transações por ID da loja e contar o número de transações em cada grupo
        transacoes_por_id_loja = df.groupby('ID Loja').size().reset_index(name='Número de Transações')
        
        # Ordenar as transações por ID da loja em ordem decrescente de número de transações
        transacoes_por_id_loja = transacoes_por_id_loja.sort_values(by='Número de Transações', ascending=False)
        
        # Exibir a tabela de transações por ID da loja
        print(transacoes_por_id_loja)
        
    except Exception as e:
        print("Ocorreu um erro ao ler o arquivo:", e)

# Chamar a função para criar a tabela
tabela_transacoes_por_id_loja()



mport pandas as pd

def tabela_transacoes_por_id_loja_com_data():
    try:
        # Ler o arquivo Excel
        df = pd.read_excel(r"C:\Users\geana\Downloads\Base Vendas - 2022.xlsx")
        
        # Exibir as primeiras linhas do DataFrame para entender sua estrutura
        print("Visualizando as primeiras linhas do DataFrame:")
        print(df.head())
        print()
        
        # Agrupar as transações por ID da loja e contar o número de transações em cada grupo
        transacoes_por_id_loja = df.groupby(['ID Loja', 'Data da Venda']).size().reset_index(name='Número de Transações')
        
        # Ordenar as transações por ID da loja e data em ordem decrescente de número de transações
        transacoes_por_id_loja = transacoes_por_id_loja.sort_values(by=['ID Loja', 'Data da Venda'], ascending=[True, True])
        
        # Exibir a tabela de transações por ID da loja com data
        print("Tabela de Transações por ID da Loja com Data:")
        print(transacoes_por_id_loja)
        
    except Exception as e:
        print("Ocorreu um erro ao ler o arquivo:", e)

# Chamar a função para criar a tabela com data de transação
tabela_transacoes_por_id_loja_com_data()




import tkinter as tk
from tkinter import ttk
from tkinter import messagebox
import pandas as pd

# Função para exibir informações do cliente
def exibir_informacoes_cliente():
    # Obter o ID do cliente digitado pelo usuário
    cliente_id = entry_id_cliente.get()
    
    try:
        # Ler o arquivo Excel
        df = pd.read_excel(r"C:\Users\geana\Downloads\Base Vendas - 2022.xlsx")
        
        # Filtrar as informações para o ID do cliente fornecido
        informacoes_cliente = df[df['ID Cliente'] == int(cliente_id)]
        
        # Verificar se há informações para o cliente
        if informacoes_cliente.empty:
            messagebox.showinfo("Informações do Cliente", f"Nenhuma informação encontrada para o ID do cliente {cliente_id}.")
        else:
            # Criar janela para exibir a tabela de informações do cliente
            janela_cliente = tk.Toplevel(root)
            janela_cliente.title(f"Informações do Cliente - ID {cliente_id}")
            
            # Criar Treeview para exibir informações do cliente
            tree = ttk.Treeview(janela_cliente)
            tree["columns"] = list(informacoes_cliente.columns)
            tree["show"] = "headings"
            
            # Adicionar colunas ao Treeview
            for col in informacoes_cliente.columns:
                tree.heading(col, text=col)
            
            # Adicionar linhas ao Treeview
            for index, row in informacoes_cliente.iterrows():
                tree.insert("", "end", values=list(row))
            
            # Adicionar scrollbar ao Treeview
            scroll_y = ttk.Scrollbar(janela_cliente, orient="vertical", command=tree.yview)
            scroll_y.pack(side="right", fill="y")
            tree.configure(yscrollcommand=scroll_y.set)
            
            tree.pack(expand=True, fill="both")
            
    except Exception as e:
        messagebox.showerror("Erro", f"Ocorreu um erro ao ler o arquivo: {e}")

# Configuração da janela principal
root = tk.Tk()
root.title("Consulta de Informações do Cliente")

# Entrada para o ID do cliente
label_id_cliente = tk.Label(root, text="Digite o ID do Cliente:")
label_id_cliente.pack()
entry_id_cliente = tk.Entry(root)
entry_id_cliente.pack()

# Botão para exibir as informações do cliente
btn_exibir_informacoes = tk.Button(root, text="Exibir Informações do Cliente", command=exibir_informacoes_cliente)
btn_exibir_informacoes.pack()

# Loop principal da aplicação
root.mainloop()
