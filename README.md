import pandas as pd
import numpy as np
import matplotlib.pyplot as plt  # Added for plotting

file_path = "/content/Actual_38.55_-75.15_2006_UPV_49MW_5_Min.xlsx"

try:
    df = pd.read_excel(file_path)
    print("File Loaded Successfully!")
    print("Columns:", df.columns.tolist())
except Exception as e:
    print(f"Error reading file: {e}")
    df = None

if df is not None:
    if "Power(MW)" in df.columns:
        df = df.dropna(subset=["Power(MW)"])
    else:
        raise ValueError("Column 'Power(MW)' not found!")

    def calculate_statistics(df):
        power = df["Power(MW)"]
        if power.empty:
            return {"mean": None, "median": None, "mode": None, "std_dev": None, "variance": None}
        mode = power.mode().iloc[0] if not power.mode().empty else None
        return {
            "mean": power.mean(),
            "median": power.median(),
            "mode": mode,
            "std_dev": power.std(ddof=0),
            "variance": power.var(ddof=0)
        }

    stats = calculate_statistics(df)
    print("\nStatistics:")
    for k, v in stats.items():
        print(f"{k.title()}: {v}")

    summary = {
        "count": len(df),
        "min": df["Power(MW)"].min(),
        "max": df["Power(MW)"].max()
    }
    print("\nSummary:")
    for k, v in summary.items():
        print(f"{k.title()}: {v}")


    plt.figure(figsize=(10, 4))
    plt.plot(df["Power(MW)"], label="Power (MW)", color='red')
    plt.title("Power (MW) Over Time")
    plt.xlabel("Time (index)")
    plt.ylabel("Power (MW)")
    plt.grid(True)
    plt.legend()
    plt.tight_layout()
    plt.show()


    try:
        threshold = float(input("\nEnter power threshold to filter: "))
        filtered = df[df["Power(MW)"] > threshold]
        print(f"{len(filtered)} values above {threshold} MW")
    except ValueError:
        print("Invalid threshold input.")

    try:
        search = float(input("Enter a power value to search (or -1 to skip): "))
        if search != -1:
            result = df[df["Power(MW)"] == search]
            if not result.empty:
                print(f"Found at rows: {result.index.tolist()}")
            else:
                print("Value not found.")
    except ValueError:
        print("Invalid search input.")
