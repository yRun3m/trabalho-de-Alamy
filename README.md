import tkinter as tk
from tkinter import messagebox

# Função para calcular a média de uma lista
def calcular_media(lista):
    return sum(lista) / len(lista)

# Função acionada ao clicar no botão
def processar_matriz():
    entrada = entrada_texto.get("1.0", tk.END).strip()
    
    if not entrada:
        messagebox.showerror("Erro", "Por favor, insira a matriz de temperaturas.")
        return

    try:
        linhas = entrada.split("\n")
        matriz = []
        for linha in linhas:
            valores = list(map(float, linha.strip().split()))
            matriz.append(valores)

        resultado_texto = ""
        for i, dia in enumerate(matriz):
            media = calcular_media(dia)
            resultado_texto += f"Dia {i+1}: {media:.2f}°C\n"

        resultado_label.config(text=resultado_texto)

    except ValueError:
        messagebox.showerror("Erro", "Certifique-se de que todos os valores sejam números separados por espaços.")

# Criando a janela
janela = tk.Tk()
janela.title("Média de Temperaturas Diárias")

# Instruções
instrucoes = tk.Label(janela, text="Insira os valores de temperatura separados por espaço.\nCada linha representa um dia:")
instrucoes.pack(pady=5)

# Caixa de texto para entrada
entrada_texto = tk.Text(janela, height=10, width=40)
entrada_texto.pack()

# Botão para calcular
botao_calcular = tk.Button(janela, text="Calcular Média", command=processar_matriz)
botao_calcular.pack(pady=10)

# Resultado
resultado_label = tk.Label(janela, text="", font=("Arial", 12), justify="left")
resultado_label.pack()

# Iniciar a interface
janela.mainloop()
