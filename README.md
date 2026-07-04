# booklist
import pandas as pd

# Load dataset
df = pd.read_csv("library_books.csv")

print("===== LIBRARY BOOKS =====")
print(df)

# Total books
print("\nTotal Books :", len(df))

# Total Copies
print("Total Copies :", df["Copies"].sum())

# Programming Books
print("\nProgramming Books")
print(df[df["Category"]=="Programming"])

# Book with Maximum Copies
max_book = df.loc[df["Copies"].idxmax()]

print("\nBook with Highest Copies")
print(max_book)

# Search Book
book = input("\nEnter Book Name : ")

result = df[df["Book_Name"].str.lower() == book.lower()]

if len(result) > 0:
    print("\nBook Found")
    print(result)
else:
    print("Book Not Found")

# Add Status Column

def status(copies):
    if copies >= 5:
        return "Available"
    elif copies >= 2:
        return "Limited"
    else:
        return "Out of Stock"

df["Status"] = df["Copies"].apply(status)

print("\nUpdated Library")
print(df)

# Save new file
df.to_csv("updated_library.csv", index=False)

print("\nFile Saved Successfully.")
