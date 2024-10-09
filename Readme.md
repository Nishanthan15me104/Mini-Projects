# Introduction


# Objective

1. To build a contact book application.
2. To build a inventory Management System
3. To load and get basic descriptive statistics of a stock
4. To Analysis the stock data using followig charts
        - Moving average trend
        - Daily Return Histogram 
        - Volume vs Price 

# Tools I Used

For my deep dive into the data analyst job market, I harnessed the power of several key tools:

- **Python:** The backbone of my analysis, allowing me to analyze the data and find critical insights.I also used the following Python libraries:
    - **Pandas Library:** This was used to analyze the data. 
    - **Matplotlib Library:** I visualized the data.
    - **Seaborn Library:** Helped me create more advanced visuals. 
- **Jupyter Notebooks:** The tool I used to run my Python scripts which let me easily include my notes and analysis.
- **Visual Studio Code:** My go-to for executing my Python scripts.
- **Git & GitHub:** Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.

# The Analysis 

## Contact Management System: A Python Script

### Introduction

This Python script implements a simple contact management system that allows users to add, find, update, and delete contacts. It utilizes a CSV file (contact_new.csv) to store and retrieve contact information.

### Key Features:

- **Contact Storage:** Uses a CSV file to store contact data, ensuring persistence and easy access.
Data Validation: Enforces data integrity by validating user input for name, phone number, address, and remarks.
Contact Management Operations: Provides options to add, find, update, and delete contacts.
User-Friendly Interface: Presents a simple menu-driven interface for easy interaction.
Code Breakdown:

File Handling:

load_contact(): Loads contact data from the CSV file if it exists or creates a new DataFrame if the file doesn't exist.
save_contacts(df): Saves the updated DataFrame to the CSV file.
Contact Operations:

add_contact(df): Prompts the user for contact details, validates the input, and adds a new contact to the DataFrame.
find_contact(df): Searches for a contact by name and displays the matching contact information.
update_contact(df): Allows users to update the phone number, address, or remarks for an existing contact.
delete_contact(df): Deletes a contact from the DataFrame based on the provided name.
Main Loop:

The main() function provides a menu-driven interface for users to interact with the contact management system. It continuously prompts the user for input until they choose to exit.
Usage:

Save the script as a Python file (e.g., contact_manager.py).
Run the script using a Python interpreter.
Follow the on-screen prompts to add, find, update, or delete contacts.
Additional Notes:

You can customize the data fields and validation logic to suit your specific requirements.
Consider adding error handling and logging to improve the robustness of the script.
You might explore using a database like SQLite for more complex data management needs.
This script provides a basic foundation for a contact management system. You can extend it with additional features like searching by phone number, grouping contacts, or integrating with other applications.

## Inventory Management System

## Stock Analysis 

### Descriptive Analysis


