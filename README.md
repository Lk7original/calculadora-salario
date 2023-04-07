# calculadora-salario
import tkinter as tk

class CalculadoraSalario:
    def __init__(self, master):
        self.master = master
        master.title("Calculadora de Salário")

        self.valor_hora_label = tk.Label(master, text="Valor da hora:")
        self.valor_hora_label.grid(row=0, column=0)

        self.valor_hora_entry = tk.Entry(master)
        self.valor_hora_entry.grid(row=0, column=1)

        self.dias_trabalhados_label = tk.Label(master, text="Dias trabalhados:")
        self.dias_trabalhados_label.grid(row=1, column=0)

        self.dias_trabalhados_entry = tk.Entry(master)
        self.dias_trabalhados_entry.grid(row=1, column=1)

        self.horas_por_dia_labels = []
        self.horas_por_dia_entries = []

        for i in range(7):
            label = tk.Label(master, text=f"Horas no dia {i+1}:")
            label.grid(row=i+2, column=0)

            entry = tk.Entry(master)
            entry.grid(row=i+2, column=1)

            self.horas_por_dia_labels.append(label)
            self.horas_por_dia_entries.append(entry)

        self.calcular_button = tk.Button(master, text="Calcular", command=self.calcular_salario)
        self.calcular_button.grid(row=102, column=0, columnspan=2)

        self.resultado_label = tk.Label(master, text="")
        self.resultado_label.grid(row=103, column=0, columnspan=2)

    def calcular_salario(self):
        try:
            valor_hora = float(self.valor_hora_entry.get())
            dias_trabalhados = int(self.dias_trabalhados_entry.get())

            total_horas_trabalhadas = 0
            for i in range(dias_trabalhados):
                horas_trabalhadas = float(self.horas_por_dia_entries[i].get())
                total_horas_trabalhadas += horas_trabalhadas

            salario_total = valor_hora * total_horas_trabalhadas

            self.resultado_label.config(text=f"Salário total: R${salario_total:.2f}", fg="green")
        except ValueError:
            self.resultado_label.config(text="Preencha todos os campos corretamente.", fg="red")

# Cria a janela principal
janela = tk.Tk()

# Cria a instância da calculadora de salário
calculadora = CalculadoraSalario(janela)

# Inicia o loop da janela
janela.mainloop()
