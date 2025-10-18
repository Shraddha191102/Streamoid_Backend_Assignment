# Streamoid_Backend_Assignment - Product Catalog API 

Hey! This is my backend project for the Streamoid take-home exercise.

It's a simple API built with Flask that lets you upload a product catalog (as a CSV or Excel file). It checks the file for errors, saves all the good products to a database, and then lets you list or search for them.

## What it does

* **Upload Files:** You can `POST` a `.csv` or `.xlsx` file to the `/upload` endpoint.
* **Validate Data:** It checks every single row in your file to make sure...
    * Required fields like `sku`, `name`, `brand`, `mrp`, and `price` are all there.
    * The `price` is less than or equal to the `mrp`.
    * The `quantity` is 0 or more.
* **Save to DB:** All the valid products get saved into a local SQLite database (`products.db`).
* **List Products:** You can `GET` all the products from the database using the `/products` endpoint (it even has pagination!).
* **Search Products:** You can use `/products/search` to filter by brand, color, or price range.

---

## How to Get it Running 

You'll just need **Python 3** installed.


    ```

1.  **Create a Virtual Environment:**
    (This is a good habit to keep all the packages separate!)
    ```bash
    # On Mac/Linux
    python3 -m venv venv
    source venv/bin/activate
    
    # On Windows
    python -m venv venv
    .\venv\Scripts\activate
    ```

2.  **Install the Packages:**
    This project needs Flask (for the server) and openpyxl (to read Excel files).
    ```bash
    pip install flask openpyxl
    ```

3.  **Run the App:**
    ```bash
    python app.py
    ```
    (Assuming your main file is named `app.py`)

    That's it! The server will start up and be running on `http://localhost:5000`.

---

## API Endpoints Endpoints Documentation

Here are the endpoints you can use (I used Postman to test them).

### 1. Upload Products

Upload your product file here. It will check every row, save the good ones, and tell you which ones failed (if any).

* **Endpoint:** `POST /upload`
* **Body:** `form-data`
* **Key:** `file`
* **Value:** (Select your `.csv` or `.xlsx` file)

**Example cURL Request:**
```bash
curl -X POST -F "file=@products.csv" http://localhost:5000/upload
