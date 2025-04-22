import tkinter as tk
from tkinter import messagebox
import yfinance as yf

root = tk.Tk()
root.title("Stock Portfolio Manager")
root.geometry("350x400")

portfolio = {}

def add_stock():
    ticker = ticker_entry.get().upper()
    quantity = quantity_entry.get()

    if not ticker or not quantity.isdigit():
        messagebox.showerror("Error", "Enter a valid stock ticker and quantity!")
        return

    portfolio[ticker] = int(quantity)
    messagebox.showinfo("Success", f"Added {quantity} shares of {ticker}")

def get_stock_price(ticker):
    try:
        stock = yf.Ticker(ticker)
        price = stock.history(period="1d")["Close"].iloc[-1]
        return round(price, 2)
    except:
        return None

def show_portfolio():
    if not portfolio:
        messagebox.showinfo("Portfolio", "No stocks added yet!")
        return

    total_value = 0
    portfolio_text = "Portfolio:\n"

    for ticker, quantity in portfolio.items():
        price = get_stock_price(ticker)
        if price:
            stock_value = price * quantity
            total_value += stock_value
            portfolio_text += f"{ticker}: {quantity} shares @ ₹{price} each → ₹{stock_value}\n"
        else:
            portfolio_text += f"{ticker}: Price not available\n"

    portfolio_text += f"\nTotal Portfolio Value: ₹{total_value}"
    messagebox.showinfo("Portfolio Value", portfolio_text)

tk.Label(root, text="Stock Ticker:").pack(pady=5)
ticker_entry = tk.Entry(root)
ticker_entry.pack(pady=5)

tk.Label(root, text="Quantity:").pack(pady=5)
quantity_entry = tk.Entry(root)
quantity_entry.pack(pady=5)

tk.Button(root, text="Add Stock", command=add_stock).pack(pady=10)
tk.Button(root, text="Show Portfolio", command=show_portfolio).pack(pady=10)

root.mainloop()
