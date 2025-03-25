# Amazon Sales Report #
## Program ##
```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

def load_and_clean_data(file_path):
    # Load dataset
    df = pd.read_csv(file_path)
    
    # Convert Date column to datetime
    df["Date"] = pd.to_datetime(df["Date"], errors="coerce")
    
    # Fill missing values
    df["Amount"].fillna(0, inplace=True)
    df["currency"].fillna("INR", inplace=True)
    
    # Convert ship-postal-code to string
    df["ship-postal-code"] = df["ship-postal-code"].astype(str).str.replace(".0", "", regex=False)
    
    return df

def plot_sales_trend(df):
    plt.figure(figsize=(12, 6))
    df.groupby("Date")["Amount"].sum().plot(marker="o", color="b")
    plt.title("Total Sales Amount Over Time", fontsize=14)
    plt.xlabel("Date", fontsize=12)
    plt.ylabel("Total Sales (INR)", fontsize=12)
    plt.xticks(rotation=45)
    plt.show()

def plot_top_categories(df):
    top_categories = df["Category"].value_counts().head(10)
    plt.figure(figsize=(12, 6))
    sns.barplot(x=top_categories.index, y=top_categories.values, palette="viridis")
    plt.title("Top 10 Selling Product Categories", fontsize=14)
    plt.xlabel("Product Category", fontsize=12)
    plt.ylabel("Number of Orders", fontsize=12)
    plt.xticks(rotation=45)
    plt.show()

def plot_fulfillment_methods(df):
    fulfillment_counts = df["fulfilled-by"].value_counts()
    plt.figure(figsize=(8, 5))
    sns.barplot(x=fulfillment_counts.index, y=fulfillment_counts.values, palette="coolwarm")
    plt.title("Fulfillment Method Distribution", fontsize=14)
    plt.xlabel("Fulfillment Method", fontsize=12)
    plt.ylabel("Number of Orders", fontsize=12)
    plt.xticks(rotation=45)
    plt.show()

def main():
    file_path = "Amazon Sale Report.csv"  # Update with the correct path
    df = load_and_clean_data(file_path)
    
    # Generate visualizations
    plot_sales_trend(df)
    plot_top_categories(df)
    plot_fulfillment_methods(df)

if __name__ == "__main__":
    main()
```
## OUTPUT;

![image](https://github.com/user-attachments/assets/247f43da-6d73-46a2-b976-3d9df41a0af3)

![image](https://github.com/user-attachments/assets/07d3f1cc-85ad-45e7-b11d-a58f1d060806)

![image](https://github.com/user-attachments/assets/a9782c35-dff9-4091-ab63-043a0a04e8fd)




