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
- **Contact Management Operations:** Provides options to add, find, update, and delete contacts.
- **User-Friendly Interface:** Presents a simple menu-driven interface for easy interaction.

###Code Breakdown:

#### File Handling:

- **load_contact():** Loads contact data from the CSV file if it exists or creates a new DataFrame if the file doesn't exist.

'''

    def load_contact():                                                           # To load contact if available or create
    if os.path.exists(file_save):
        df = pd.read_csv(file_save)
        print ('contacts loaded successfully')
    else:
        df= pd.DataFrame(columns=['Name','Phone_Number','Address','Remarks'])
    return df


- **save_contacts(df):** Saves the updated DataFrame to the CSV file.

'''

    def save_contacts(df):
        df.to_csv(file_save, index=False)
        print ('contact saved succesfully')


#### Contact Operations:

- **add_contact(df):** Prompts the user for contact details, validates the input, and adds a new contact to the DataFrame.

'''
    ef add_contact(df):
    
    Name = input('Enter Name : ')
    Phone_Number = input('Enter Phone Number : ')
    Address = input('Enter Address :')
    Remarks = input('Enter Remarks : ')

    if not isinstance(Name,str) or not Name:
        raise ValueError('Name must be a non - empty string')
    if not isinstance(Phone_Number,str) or not Phone_Number:
        raise ValueError('Phone_Number must be a non - empty string')
    if not isinstance(Address,str):
        raise ValueError('Address must be a non - empty string')
    if not isinstance(Remarks,str):
        raise ValueError('Remarks must be a non - empty string')
    
    if Name in df['Name'].values:
        raise ValueError('Enter Name already exsist in contact list.')
    if Name in df['Phone_Number'].values:
        raise ValueError('Enter Name already exsist in contact list.')
    
    new_contact =pd.Series({
        'Name' : Name,
        'Phone_Number' : Phone_Number,
        'Address' : Address,
        'Remarks' : Remarks
    })

    df = pd.concat([df,new_contact.to_frame().T], ignore_index =True)
    save_contacts(df)
    print('contact added successfully.')

    return df 

- **find_contact(df):** Searches for a contact by name and displays the matching contact information.

'''

    def find_contact(df):
    """Finds a contact by name in the DataFrame."""
    Name = input("Enter the name to search: ")
    contact = df[df['Name'] == Name]
    if contact.empty:
        print("Contact not found.")
    else:
        print(contact)


- **update_contact(df):** Allows users to update the phone number, address, or remarks for an existing contact.

'''

    def update_contact(df):

    Name = input('Enter New Name : ')

    if not isinstance(Name,str) or not Name:
        raise ValueError('Name must be a non - empty string, Enter Valid Name')
    contact = df[df['Name'] == Name]
    if contact.empty:     
        print('contact not fount')
    else:
        New_Phone_Number = input('Enter Phone Number : ')
        New_Address = input('Enter Address :')
        New_Remarks = input('Enter Remarks : ')

    if not isinstance(New_Phone_Number,str) or not New_Phone_Number:
        raise ValueError('New_Phone_Number must be a non - empty string')
    if not isinstance(New_Address,str):
        raise ValueError('New_Address must be a non - empty string')
    if not isinstance(New_Remarks,str):
        raise ValueError('New_Remarks must be a non - empty string')

    df.loc[df['Name'] == Name,['Phone_Number','Address','Remarks']] = [New_Phone_Number,New_Address,New_Remarks]
    save_contacts(df)
    print("Contact updated successfully.")
    return df


- **delete_contact(df):** Deletes a contact from the DataFrame based on the provided name.
Main Loop:

'''
    def delete_contact(df):
    """Deletes a contact from the DataFrame."""
    name = input("Enter the name of the contact to delete: ")
    if name not in df['Name'].values:
        print("Contact not found.")
    else:
        df = df[df['Name'] != name]
        save_contacts(df)
        print("Contact deleted successfully.")
    return df

- **The main()** function provides a menu-driven interface for users to interact with the contact management system. It continuously prompts the user for input until they choose to exit.

'''

    def main():
    df = load_contact()
    while True:
        print ('/n Contact Management System')
        print("1. Add Contact")
        print("2. Find Contact")
        print("3. Update Contact")
        print("4. Delete Contact")
        print("5. View All Contacts")
        print("6. Exit")

        choice = input('Enter your choice')

        if choice == '1':
            df = add_contact(df)
        elif choice == '2':
            df = find_contact(df)
        elif choice == '3':
            df = update_contact(df)
        elif choice == '4':
            df = delete_contact(df)
        elif choice == '5':
            print("\nAll Contacts:")
            print(df)
        elif choice == '6':
            break
        else:
            print("Invalid choice. Please try again.")

    print("Goodbye!")

if __name__ == "__main__":
    main()

#### Usage:

- Save the script as a Python file 

- Run the script using a Python interpreter.

- Follow the on-screen prompts to add, find, update, or delete contacts.

- This script provides a basic foundation for a contact management system.


## Inventory Management System: A Python Script

### Introduction

This Python script provides a basic inventory management system that allows users to add, find, update, delete, and track the quantity of products in inventory. It utilizes a CSV file (inventory.csv) to store and retrieve inventory data.

### Key Features:

- **Inventory Tracking:** Manages product names, quantities, and prices.
- **Data Validation:** Ensures data integrity by validating user input.
- **File Persistence:** Saves inventory data to a CSV file for future reference.
- **User-Friendly Interface:** Provides a simple menu-driven interface for easy interaction.

### Code Breakdown:

#### File Handling:

- **load_inventory():** Loads inventory data from the CSV file or creates a new DataFrame if the file doesn't exist.

    def load_inventory():                                                           # To load Item if available or create
    if os.path.exists(file_save):
        df = pd.read_csv(file_save)
        print ('Inventory loaded successfully')
    else:
        df= pd.DataFrame(columns=['Product','Quantity','Price'])
    return df

- **save_product(df):** Saves the updated DataFrame to the CSV file.


    def save_product(df):
    df.to_csv(file_save, index =False)
    print('Inventory saved successfully')

#### Product Operations:

- **add_product(df):** Prompts the user for product details, validates input, and adds a new product to the DataFrame.

    
        def add_product(df):

        Product  = input('Enter the Product')
        Quantity = input('Enter quantity')
        Price = input('Enter price')

        if not isinstance(Product,str) or not Product:
            raise ValueError('Product must me non-empty string')
        try:
            Quantity = int(Quantity)
        except ValueError:
        raise ValueError('Quantity must be an integer')

        try:
            Price = float(Price)
        except ValueError:
            raise ValueError('Price must be a float')
        
        if Product in df['Product'].values:
            raise ValueError('Product already exsist')
        
        new_product = pd.Series({
            'Product' : Product,
            'Quantity' : Quantity,
            'Price' : Price
        })

        df = pd.concat([df,new_product.to_frame().T], ignore_index =True)
        save_product(df)
        print('New product added')

        return df

- **delete_product(df):** Deletes a product from the DataFrame based on the provided name.

        def delete_product(df):
        Product = input('Enter product')
        find_product = df[df['Product'] == Product]
        if find_product.empty:
            print('No product found')
        else:
            df = df[df['Product'] != Product]
            save_product(df)
            print('Product deleted successfully')
            return df    

- **find_product(df):** Searches for a product by name and displays its details.

        def find_product(df):

        Product = input('Enter product')
        display_product = df[df['Product'] == Product]
        if display_product.empty:
            print('No product found')
        else:
            print(display_product)

- **update_stock(df):** Updates the quantity of a product based on sales or purchases.

        def update_stock(df):
        sell_product = input('Enter product : ')
        quantity_sold = input('Enter quantity :')
        quantity_sold = int(quantity_sold)

        Product = df[df['Product'] == sell_product]

        quantity = Product['Quantity'].iloc[0]

        quantity_change = quantity - quantity_sold

        if not isinstance(sell_product,str)  or not sell_product:
            raise ValueError('Product must me non-empty string')
        
        if sell_product not in df['Product'].values: 
            raise ValueError('Product not available in inventory')
        
        if quantity_sold > quantity:
            raise ValueError('Quantity provided cannot be more than available Quantity')

        df.loc[df['Product'] == sell_product,'Quantity'] = quantity_change
        save_product(df)

        print('Sale data updated')
        return df 
       

- **return_stock(df):** Updates the quantity of a product based on returns.

        def return_stock(df):

            return_stock      = input('Enter the product :')
            quantity_returned = input('Enter number of quantity :')
            
            if not isinstance(return_stock,str)  or not return_stock:
                raise ValueError('Product must me non-empty string')
            try:
                quantity_returned = int(quantity_returned)  # Ensure it's an integer
            except ValueError:
                raise ValueError('Quantity must be an integer')
            
            if return_stock not in df['Product'].values: 
                raise ValueError('Product not available in inventory')

            new_return_stock = df[df['Product'] == return_stock]
            
            curr_number_qt = new_return_stock['Quantity'].iloc[0]

            new_number_qt = curr_number_qt - quantity_returned

            df.loc[df['Product'] == return_stock,'Quantity'] = new_number_qt
            save_product(df)

            print(f'Updated stock for {return_stock}: {new_number_qt}')
            return df

- **total_stock(df):** Calculates the total stock in inventory.

        def total_stock(df):

            total_stock = df['Quantity'].sum()

            print(f'Total stock in inventory : {total_stock}')


#### Main Loop:

- **The main()** function provides a menu-driven interface for users to interact with the inventory management system. It continuously prompts the user for input until they choose to exit.

        def main():   
            df = load_inventory()
            while True:
                print ('\n Inventory Management System')
                print("1. Add Item")
                print("2. Find Item")
                print("3. Update Item")
                print("4. Delete Item")
                print("5. Purchase Update")
                print("6. Return update")

                print("7. Return stock total")
                print("8. exit")

                choice = input ('Enter your choice')

                if choice == '1':
                    df = add_product(df)
                elif choice == '2':
                    find_product(df)
                elif choice == '3':
                    df = update_stock(df)
                elif choice == '4':
                    df = delete_product(df)
                elif choice == '5':
                    df = purchase_stock(df)
                elif choice == '6':
                    df = return_stock(df)
                elif choice == '7':
                    df = total_stock(df)
                elif choice == '8':
                    break 
                else:
                    print("Invalid choice. Please try again.")

        if __name__ == '__main__':
            main()


#### Usage:

- Save the script as a Python file 
- Run the script using a Python interpreter.
- Follow the on-screen prompts to add, find, update, or delete products and track inventory.

This script provides a foundation for a basic inventory management system.


## Descriptive Stock Analysis: 

### Introduction

This Python script performs descriptive statistical analysis on a given dataset of stock data. It calculates various statistical measures such as mean, median, mode, standard deviation, variance, range, skewness, and kurtosis for each numeric column in the dataset.

### Loading Data

This Python script downloads historical stock data for a specified ticker symbol and saves it as an Excel file for further analysis. It utilizes the yfinance library to fetch financial data and pandas for data manipulation and file handling.

- **Data Acquisition:** Downloads historical stock data using the yfinance library.
- **User-Defined Ticker:** Allows users to specify the desired ticker symbol.
- **Customizable Time Range:** Enables users to define the start and end date for data retrieval.
- **Excel Output:** Saves the downloaded data to an Excel file for convenient access.

**Code Breakdown:**

- **Import Libraries:** Imports the pandas library for data manipulation and yfinance for accessing financial data.
- **Define Ticker Symbol:** Sets the variable ticker to the desired stock ticker symbol (e.g., 'HDFCBANK.NS'which is used for analysis).
- **Set Date Range:** Defines the start and end dates for data retrieval using pd.Timestamp and pd.DateOffset.
    - start: One year before the current date.
    - today: The current date.
-  **Download Stock Data:** Downloads historical stock data for the specified ticker symbol and date range using yf.download().
- **Save Data to Excel:** Saves the downloaded data as an Excel file named stock_data.xlsx using data.to_excel(). The index=False argument ensures row indices aren't saved in the Excel file

        import pandas as pd
        import yfinance as yf

        ## to load stock data using yfinance and save as excel named data
        ticker = 'HDFCBANK.NS'

        today = pd.Timestamp.today()

        start = today - pd.DateOffset(years=1)

        data = yf.download(tickers=ticker,start = start, end = today)

        ## Data saved as excel to load as data frame
        data.to_excel('stock_data.xlsx',index = False )
        # load excel as data frame 
        df = pd.read_excel('stock_data.xlsx')

### Key Features:

- **Data Loading:** Loads stock data from an Excel file using pandas.read_excel().

- **Data Cleaning:** Handles missing values by filling them with the mean of the respective column.

- **Statistical Calculations:** Calculates mean, median, mode, standard deviation, variance, range, skewness, and kurtosis for each numeric column.

- **Output Formatting:** Displays the calculated statistics in a clear and readable format.

### Code Breakdown:

- **Import Libraries:** Imports the necessary libraries pandas for data manipulation and numpy for numerical operations.
- **Load Data:** Loads the stock data from the Excel file into a pandas DataFrame.
- **Data Cleaning:**
Selects only numeric columns for analysis.
Calculates the mean for each numeric column and fills missing values with the mean.
- **Statistical Calculations:**
Calculates various statistical measures for each numeric column:
    - Mean: The average value of the column.
    - Median: The middle value of the column when sorted.
    - Mode: The most frequent value in the column.
    Standard Deviation: A measure of dispersion of the data.
    - Variance: The square of the standard deviation.
    - Range: The difference between the maximum and minimum values.
    - Skewness: A measure of the asymmetry of the distribution.
    - Kurtosis: A measure of the tailedness of the distribution.
- **Output Formatting:**
Prints the calculated statistics for each column in a clear and readable format.


        def descriptive_stock_analysis(df):

            # Select only numeric columns      ###this data cleaning is not required for provided data it is just for practice
            numerical_col = df.select_dtypes(include = [int,float]).columns

            # Calculate mean for numeric columns
            df_mean = df[numerical_col].mean()

            # Fill missing values with the calculated mean
            dff = df.fillna(df_mean)

            ##calculation of descriptive statistics of the given stock data 

            mean          = dff.mean()
            median        = dff.median()
            mode          = dff.mode()
            SD            = dff.std()
            variance      = dff.var()
            range         = dff.max() -df.min()
            skewness      = dff.skew()
            kurtosis      = dff.kurtosis()

            ## for is used to iterate over all columns and provide descriptive s\taistics

            for column, mean_value in mean.items():
            print(f"The mean of column {column} is: {mean_value:.2f}")

            for column, median_value in median.items():
            print(f"The median of column {column} is: {median_value:.2f}")
            
            for column in mode.columns:
                mode_value = mode[column].iloc[0]     # mode has multiple values this assign the first value
                print(f"The mode of column {column} is: {mode_value}")

            for column, SD_value in SD.items():
            print(f"The standard deviation of column {column} is: {SD_value:.2f}")

            for column, variance_value in variance.items():
            print(f"The varince of column {column} is: {variance_value:.2f}")
            
            for column, range_value in range.items():
            print(f"The range of column {column} is: {range_value:.2f}")

            for column, skewness_value in skewness.items():
            print(f"The skewness of column {column} is: {skewness_value:.2f}")

            for column, kurtosis_value in kurtosis.items():
            print(f"The kurtosis of column {column} is: {kurtosis_value:.2f}")


### Usage:

- Save the script as a Python file .
Place your stock data in an Excel file named stock_data.xlsx.
- Run the script using a Python interpreter.
- The script will output the descriptive statistics for each numeric column in the stock data

This script provides a foundation for basic descriptive stock analysis

## Stock Price Analysis with Moving Averages: 

### Introduction

This Python script analyzes historical stock price data and visualizes it with moving averages. It utilizes the pandas library for data manipulation, matplotlib and seaborn for plotting, and yfinance (not shown in this code) to download the data (refer to the previous section for data download).

### Code Breakdown:

- **Import Libraries:** Imports necessary libraries for data manipulation (pandas), plotting (matplotlib, seaborn), and date formatting (matplotlib.dates).
- **Load Data (Assumed):** The code assumes a DataFrame df containing stock data (date, open price, etc.) is loaded from an Excel file named stock_data.xlsx (refer to the previous section for data download steps).
- **Calculate Moving Averages:**
    - Creates a copy of the DataFrame (df_plot) to avoid modifying the original data.
    - Calculates the 50-day and 20-day moving averages for the 'Open' price column using the rolling function and stores them in new columns.
- **Data Visualization:**
    - Uses df_plot.plot() to create a line chart.
    - Sets the 'Date' column as the x-axis and 'Open', '50_day_moving_average', and '20_day_moving_average' columns as the y-axis.
- **Format x-axis:**
    - Sets the x-axis limits to exclude the first 50 data points (to avoid initial fluctuations affecting the view).
    - Formats the x-axis labels as dates using matplotlib.dates.DateFormatter.
    - Adds labels and title to the plot for clarity.
- **Display Plot:** Displays the generated line chart using plt.show().

### Sample code

    plt.xlim(start_date, None)  # Set the start date 
    date_format = mdates.DateFormatter('%Y-%m-%d') 
    plt.gca().xaxis.set_major_formatter(date_format)
    plt.xlabel('Date')
    plt.ylabel('Price')
    plt.title('Stock Price vs. 50-Day Moving Average')
    plt.legend()
    plt.show()  # Display the plot

### Image Insights

![moving_Average](stock_descriptive_analysis\images\moving_average.png)

The image depicts a line chart visualizing the stock's opening price alongside its 50-day and 20-day moving averages. This helps identify trends and potential support/resistance levels in the stock price movement.

- The 50-day moving average represents a smoother trend compared to the more volatile daily open price.
- The 20-day moving average is even more sensitive to recent price changes.
- Crossovers between the price and moving averages can signal potential trend reversals, although this is not a guaranteed trading strategy.


## Analyzing Daily Stock Returns with a Histogram: 

### Introduction

This Python script analyzes daily stock returns from an Excel file and visualizes their distribution using a histogram. It utilizes the pandas library for data manipulation, seaborn for plotting, and numpy (imported but not used in this specific code) for numerical operations.

### Code Breakdown:

- **Import Libraries:** Imports necessary libraries for data manipulation (pandas), plotting (seaborn), and scientific computing (numpy - although not used in this particular code).
- **Load Data:** Reads stock data from an Excel file named stock_data.xlsx using pd.read_excel().
- **Calculate Daily Returns:**
    - Adds a new column named 'Daily_Returns' to the DataFrame.
    - Calculates the daily percentage change in closing price using pct_change().
    Handle Missing Values: Drops rows with missing values in the DataFrame using dropna(inplace=True).
- **Filter Data (Optional):**
    - Creates a new DataFrame df_fil containing data where daily returns are within a specified range (min_value and max_value). This step is optional and filters out extreme outliers.
- **Plot Histogram:**
    - Creates a histogram using sns.histplot() to visualize the distribution of daily returns in the filtered DataFrame (df_fil).
    - Sets the number of bins (bins=30), disables kernel density estimation (kde=False), and uses a blue color.
- **Customize Plot:**
    - Adds a title, labels for the x and y-axis, and a legend for clarity.
    - Uses plt.tight_layout() to improve spacing between elements.
- **Display Plot:** Displays the generated histogram using plt.show().

**Sample Code**

    plt.figure(figsize=(10, 6))

    sns.histplot(df_fil['Daily_Returns'], bins=30, kde=False, stat='density', color='blue', label='Daily Returns')

    plt.title('Histogram of Daily Returns with Normal Distribution Curve')
    plt.xlabel('Daily Returns')
    plt.ylabel('Density')
    plt.legend()


    plt.tight_layout()
    plt.show()

### Image Insights

![histogram](stock_descriptive_analysis\images\histogram_stock.png)

The image depicts a histogram representing the distribution of daily stock returns. The x-axis shows the range of daily returns, and the y-axis shows the density (frequency) of each return value. A normal distribution curve is often used as a reference to visually assess how closely the actual data resembles a normal distribution.

- The data in this example appears to be somewhat centered around zero, with most daily returns falling within a small range around the mean.
- The absence of a tail on either side suggests the data may not perfectly follow a normal distribution, but it can be a helpful starting point for further analysis.

## Visualizing Stock Price and Volume: A Python Script

### Introduction

This Python script creates a combination chart to visualize the relationship between stock prices and trading volume over time. It utilizes the pandas library for data manipulation, matplotlib and seaborn for plotting, and matplotlib.dates for handling date-time data.

### Code Breakdown:

- **Import Libraries:** Imports necessary libraries for data manipulation (pandas), plotting (matplotlib, seaborn), and date-time handling (matplotlib.dates).
- **Load Data:** Reads stock data from an Excel file named stock_data.xlsx using pd.read_excel().
- **Convert Date to DateTime:** Converts the 'Date' column to a datetime format using pd. 
- **to_datetime()** for accurate time-series plotting.

**Create Subplots:**
- Creates a figure and a pair of subplots using 
    plt.subplots().
- Assigns the subplots to the variables ax (main) and ax1 (twin).

**Volume Bar Chart:**
- Uses ax.bar() to create a bar chart on the primary axis (ax) representing the daily trading volume.
- Sets the 'Date' column as the x-axis and the 'Volume' column as the y-axis.
- Sets the label for the bar series as 'volume' and the color to red.

**Price Line Chart:**
- Uses ax1.plot() to create a line chart on the secondary axis (ax1) representing the daily closing price.
- Sets the 'Date' column as the x-axis and the 'Close' column as the y-axis.
- Sets the label for the line series as 'Close Price'.

**Customize Plot:**
- Sets the title of the plot to 'Price vs Volume'.
- Sets the y-axis limits for the volume chart (primary axis) to range from 0 to the maximum volume value in the data.
- Sets the x-axis label for both charts to 'Date' (since they share the x-axis).

**Display Plot:** (code not shown, but assumed) Displays the generated combination chart using plt.show().

### Image Insights

![volume/price](./stock_descriptive_analysis\images\volume_price.png)

The image depicts a combination chart where the primary axis (left-hand side) shows a bar chart representing the daily trading volume, and the secondary axis (right-hand side) shows a line chart representing the daily closing price. Both charts share the same x-axis (date).

- This visualization allows you to observe potential correlations between price movements and trading volume.
- High volume bars often coincide with significant price changes, either up or down, indicating periods of increased trading activity.
- Lower volume bars may suggest quieter trading periods with smaller price fluctuations.

This script provides a basic example of creating a combination chart to visualize stock price and volume. You can adapt and extend it to suit your specific needs and incorporate additional data or analysis techniques.