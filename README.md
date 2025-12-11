import tkinter as tk
from tkinter import messagebox
import pandas as pd
 
class InventoryApp:
    def __init__(self, master):
        self.master = master
        self.master.title("Система учета расходных материалов на складе")
        self.labels = ['Вид материала', 'Размер катушки, вес кг.', 'Сечение', 'Цвет', 'Статус', 'Остаток']
        self.entries = []
        for i, label in enumerate(self.labels):
            tk.Label(master, text = label).grid(row = i, column = 0)
            entry = tk.Entry(master)
            entry.grid(row = i, column = 1)
            self.entries.append(entry)
        self.add_button = tk.Button(master, text = "Добавить", command = self.add_item)
        self.add_button.grid(row = len(self.labels), columnspan = 2)
        self.save_button = tk.Button(master, text = "Сохранить в Excel", command = self.save_to_excel)
        self.save_button.grid(row = len(self.labels) + 1, columnspan = 2)
 
        self.inventory = []
    def add_item(self):
        item = {label: entry.get() for label, entry in zip(self.labels, self.entries)}
        self.inventory.append(item)
        messagebox.showinfo("Успех", "Материал добавлен!")
        for entry in self.entries:
            entry.delete(0, tk.END)
 
    def save_to_excel(self):
        df = pd.DataFrame(self.inventory)
        df.to_excel('inventory.xlsx', index=False)
        messagebox.showinfo('Успех', 'Данные сохранены в inventory.xlsx!')
if __name__ == 'main':
    root = tk.Tk()
    app = InventoryApp(root)
    root.mainloop()
Представленный код приложения позволяет пользователям вводить информацию о товарах и сохранять данные.
