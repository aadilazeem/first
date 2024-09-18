# 
import tkinter as tk
from tkinter import messagebox

class MeterReadGUI:
    def __init__(self, root):
        self.root = root
        self.root.title("Meter Reading")

        # Create labels and entry boxes for previous and recent readings
        self.prev_label = tk.Label(root, text="Enter Previous Reading:")
        self.prev_label.grid(row=0, column=0)
        self.prev_entry = tk.Entry(root)
        self.prev_entry.grid(row=0, column=1)

        self.rec_label = tk.Label(root, text="Enter Recent Reading:")
        self.rec_label.grid(row=1, column=0)
        self.rec_entry = tk.Entry(root)
        self.rec_entry.grid(row=1, column=1)

        # Button to calculate bill
        self.calc_button = tk.Button(root, text="Calculate Bill", command=self.generate_bill)
        self.calc_button.grid(row=2, columnspan=2)

        # Label to display results
        self.result_label = tk.Label(root, text="")
        self.result_label.grid(row=3, columnspan=2)

    def read_meter(self):
        self.previous_reading = int(self.prev_entry.get())
        self.recent_reading = int(self.rec_entry.get())
        self.reading_difference = self.recent_reading - self.previous_reading
        return self.reading_difference

    def calculate_metre_cost(self):
        if self.reading_difference < 21:
            return 0 * self.reading_difference
        if self.reading_difference < 31:
            return 20*3 + (self.reading_difference - 20)*6.50
        if self.reading_difference < 51:
            return 20*3 + 10*6.50 + (self.reading_difference - 30)*8
        if self.reading_difference < 101:
            return 20*3 + 10*6.50 + 20*8 + (self.reading_difference - 50)*9.50
        if self.reading_difference < 251:
            return 20*3 + 10*6.50 + 20*8 + 50*9.50 + (self.reading_difference - 100)*9.5
        else:
            return 20*3 + 10*6.50 + 20*8 + 50*9.50 + 150*9.50 + (self.reading_difference - 250)*11

    def calculate_service_charges(self):
        if self.reading_difference < 21:
            return 30
        if self.reading_difference < 51:
            return 50
        if self.reading_difference < 101:
            return 75
        if self.reading_difference < 251:
            return 100
        else:
            return 150

    def generate_bill(self):
        try:
            difference = self.read_meter()
            total_cost = self.calculate_metre_cost()
            total_service_charges = self.calculate_service_charges()
            total_bill = total_cost + total_service_charges

            self.result_label.config(text=f"Reading Difference: {difference}\nTotal Cost: {total_bill}")
        except ValueError:
            messagebox.showerror("Input Error", "Please enter valid numeric values.")

# Create the main window
root = tk.Tk()
app = MeterReadGUI(root)
root.mainloop()
<br>
Author - Aadil Azeem
