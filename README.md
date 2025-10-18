# Streamoid_Backend_Assignment - Product Catalog API 

Hey! This is my backend project for the Streamoid take-home exercise.

It's a simple API built with Flask that lets you upload a product catalog (as a CSV or Excel file). It checks the file for errors, saves all the good products to a database, and then lets you list or search for them. It's built for reliability, ensuring that only good data makes it into the catalog.

## What it does

* **Upload Files:** You can `POST` a `.csv` or `.xlsx` file to the `/upload` endpoint.
* **Validate Data:** It checks every single row in your file to make sure...
    * Required fields like `sku`, `name`, `brand`, `mrp`, and `price` are all there.
    * The `price` is less than or equal to the `mrp`.
    * The `quantity` is 0 or more.
* **Save to DB:** All the valid products get saved into a local SQLite database (`products.db`).
* **List Products:** You can `GET` all the products from the database using the `/products` endpoint (it even has pagination!).
* **Search Products:** You can use `/products/search` to filter by brand, color, or price range.

## Technologies Used

* **Backend Framework:** Flask (Python) – Chosen for its lightweight, modular nature, allowing for rapid development of the core API endpoints.
* **Data Processing:** Pandas – The heavy-hitter for efficiently reading and processing large product catalog files (.csv, .xlsx) and performing vectorized validation checks.
* **Database:** SQLite – Used as a simple, file-based database (products.db) for persistence, making setup virtually instantaneous.
* **Database ORM:** SQLAlchemy – Provides an object-relational mapping layer for clean, Pythonic interaction with the database.

---

## How to Get it Running 

You'll just need **Python 3** installed.

1.  **Create a Virtual Environment:**

2.  **Install the Packages:**

3.  **Run the App:**
    ```bash
    python app.py
    ```
    (Assuming your main file is named `app.py`)

    That's it! The server will start up and be running on `http://localhost:5000`.

## API Endpoints Endpoints Documentation

Here are the endpoints you can use (I used Postman to test them).

### 1. Upload Products

Upload your product file here. It will check every row, save the good ones, and tell you which ones failed (if any).

* **Endpoint:** `POST /upload`
* **Body:** `form-data`
* **Key:** `file`
* **Value:** (Select your `.csv` or `.xlsx` file)

### 2. List All Products (Paginated)

Retrieve a list of all products saved in the database.
* **Endpoint:** GET /products
* **Method:** GET
* **Query Parameters (Optional):**
    * **page:** Page number to retrieve (Default: 1)
    * **limit:** Products per page (Default: 10)
 
  
### 3. Search Products

Filter the product catalog based on combined criteria.

* **Endpoint:** GET /products/search
* **Method:** GET
* **Query Parameters (Optional - can be combined):**
     * **brand:** Filter by product brand (e.g., brand=Nike)
     * **color:** Filter by product color (e.g., color=Red)
     * **minPrice:** Minimum price (e.g., minPrice=10.00)
     * **maxPrice:** Maximum price (e.g., maxPrice=50.00)

### 4. Health Check

A simple route to ensure the API service is up and running.
**Endpoint:** GET /health
**Method:** GET
**Response:** {"status": "ok"}

**Example URL Request:**

![WhatsApp Image 2025-10-18 at 15 18 08_3bc2d00e](https://github.com/user-attachments/assets/58b5951f-e51b-4e56-a201-5f34fb419e1e)

![WhatsApp Image 2025-10-18 at 15 20 57_b840cd22](https://github.com/user-attachments/assets/cc2f7191-e354-49c7-b915-1b352b4d5406)

