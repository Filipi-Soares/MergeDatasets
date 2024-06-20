# MergeDatasets

pip install pandas openpyxl

import pandas as pd

def merge_datasets(file_paths, output_file):
    """
    Merges multiple Excel files into a single CSV file.

    Parameters:
    - file_paths (list of str): List of file paths to the Excel files to be merged.
    - output_file (str): Path to the output CSV file.

    This function reads each Excel file specified in the file_paths list into a Pandas DataFrame,
    concatenates all the DataFrames into a single DataFrame, and then saves the merged DataFrame 
    to a CSV file specified by output_file.

    Example:
    file_paths = [
        r"C:\path\to\file1.xlsx",
        r"C:\path\to\file2.xlsx",
        r"C:\path\to\file3.xlsx"
    ]
    output_file = r"C:\path\to\output.csv"
    merge_datasets(file_paths, output_file)
    """
    # Initialize an empty list to hold the dataframes
    dataframes = []
    
    # Loop through each file and read it into a dataframe, then append to the list
    for file in file_paths:
        df = pd.read_excel(file, engine='openpyxl')
        dataframes.append(df)
    
    # Concatenate all dataframes into a single dataframe
    merged_df = pd.concat(dataframes, ignore_index=True)
    
    # Save the merged dataframe to a new CSV file
    merged_df.to_csv(output_file, index=False)
    print(f'Merged data saved to {output_file}')

# Example usage
file_pattern = 'C:/path/to/your/excel/files/*.xlsx'  # Replace with your file path
output_file = 'C:/path/to/save/merged_data.csv'  # Replace with your output file path
merge_datasets(file_pattern, output_file)
