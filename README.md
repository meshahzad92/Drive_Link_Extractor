# Drive Link Extractor

Drive Link Extractor is a Python-based tool that automates the process of extracting and updating Google Drive file links in CSV files. It scans through specified Google Drive folders, matches image file names based on HYPERLINK formulas present in your CSV, and outputs an updated CSV with clickable Google Drive links.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)

## Features

- **Automated Link Extraction:**  
  Scans through one or more Google Drive folders recursively to find matching image files.
  
- **CSV Update:**  
  Reads your CSV file (e.g., `leads_combined.csv`), extracts the image file name from a HYPERLINK formula, and updates or adds a new column with the corresponding Google Drive link.
  
- **Google Colab Compatible:**  
  Utilizes Google Colab’s built-in authentication methods for seamless integration when running in the Colab environment.
  
- **Robust & Recursive:**  
  The script supports recursive searching within folders, ensuring that nested files are not missed.

## Installation

Ensure you have [Python 3.x](https://www.python.org/downloads/) installed on your system.

Clone the repository:

```sh
git clone https://github.com/yourusername/drive-link-extractor.git
cd drive-link-extractor
```

Install the required dependencies using pip:

```sh
pip install pandas google-auth google-auth-oauthlib google-auth-httplib2 google-api-python-client
```

> **Note for Google Colab Users:**  
> Google Colab comes with many of these libraries pre-installed. You might only need to run an upgrade command if necessary.

## Usage

1. **Set Up Credentials:**

   - Ensure you have a valid `credentials.json` file.  
   - For Google Colab, the script uses the built-in `google.colab.auth` for authentication, so you don’t need to worry about local browser authentication issues.

2. **Prepare Your CSV File:**

   - Your CSV (e.g., `leads_combined.csv`) should include a column named `ScreenShot` containing HYPERLINK formulas in the format:
     ```
     =HYPERLINK("screenshots\YourImage.png")
     ```
   - The script will extract the image name (e.g., `YourImage.png`) and search for it in the specified Google Drive folders.

3. **Run the Script:**

   - In your terminal (or in a Colab notebook cell), run:
     ```sh
     python Drive_Link_Extractor.py
     ```
   - The updated CSV will be saved as `updated_leads_combined.csv`.

## How It Works

1. **Authentication:**  
   The script checks for saved credentials in `token.pickle`. If not found or expired, it authenticates the user using Colab’s built-in authentication methods and saves the credentials for future runs.

2. **File Listing:**  
   It recursively scans through the provided Google Drive folder IDs to list all files and subfolders.

3. **Image Matching:**  
   The tool extracts the image name from the CSV’s HYPERLINK formula and performs a case-insensitive search among the Google Drive files.

4. **CSV Updating:**  
   If a matching file is found, its `webViewLink` is inserted into a new column (`Drive Link`) in the CSV. Otherwise, the script marks the entry as "Image not found".

## Contributing

Contributions are welcome! If you have suggestions, bug fixes, or improvements, please fork the repository and submit a pull request. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgements

- Thanks to the developers of the [Google API Python Client](https://github.com/googleapis/google-api-python-client) for their invaluable work.
- Special thanks to the Google Colab team for making it easy to authenticate and run these scripts in a cloud environment.

