# Excel <-> CSV Converter

Python script that converts CSV files to Excel and Excel files to CSV.

The script supports direct command-line arguments and configuration loading from a JSON file.

## Features

- Convert CSV files to Excel `.xlsx`
- Convert Excel `.xls` and `.xlsx` files to CSV
- Export one CSV file per Excel worksheet
- Process a specific list of files
- Process all supported files in a folder
- Custom delimiter for CSV output
- Optional overwrite mode
- JSON configuration file support
- Automatic output folders
- Operation log generation

## Requirements

- Python 3
- pandas
- openpyxl

## Installation

```python
pip install pandas openpyxl
```

## JSON configuration example

```json
{
  "path": "C:/data",
  "file_list": "ALL",
  "csv_delimiter": ";",
  "force_overwrite": true
}
```

## Usage

Convert all files inside the `/data` directory:

```python
python ExcelCSVConverter.py -P "/data" -L ALL
```

Convert only the specified files inside the `/data` directory:

```python
python ExcelCSVConverter.py -P "/data" -L "file1.csv,file2.xlsx"
```

Run the conversion using the parameters defined in `config.json`:

```python
python ExcelCSVConverter.py --config config.json
```

Convert all files inside the `/data` directory and force the conversion/overwrite behavior:

```python
python ExcelCSVConverter.py -P "/data" -L ALL -F
```

## Output

The script creates:

- `<path>/CSV/` <br>
- `<path>/XLSX/` <br>
- `<path>/logConverter_<timestamp>.log`

## Example files

The [examples](examples/) folder contains a sample CSV with five fictional products, the converted Excel workbook, and the conversion log:

| File | Description |
| --- | --- |
| [products.csv](examples/products.csv) | Input data with the columns `Product`, `Category`, `Quantity`, and `Price`. |
| [products.xlsx](examples/XLSX/products.xlsx) | Excel output, with the product data in `Sheet1`. |
| [Conversion log](examples/logConverter_20260925_184757.log) | Log of the sample CSV-to-Excel conversion. |

The input CSV uses commas as separators and a period for decimal values:

```csv
Product,Category,Quantity,Price
Keyboard,Accessories,15,29.90
Mouse,Accessories,25,14.50
Monitor,Displays,8,189.99
USB Cable,Accessories,40,5.90
Webcam,Accessories,12,49.00
```

To run the example from the project directory:

```bash
python ExcelCSVConverter.py -P examples -L products.csv
```

The Excel file is written to `examples/XLSX/products.xlsx`. Since the sample output is already included, the script skips it unless you add `-F` to overwrite it:

```bash
python ExcelCSVConverter.py -P examples -L products.csv -F
```

Each run creates a log in `examples/` named `logConverter_<timestamp>.log`.

To try the reverse conversion with a semicolon delimiter:

```bash
python ExcelCSVConverter.py -P examples/XLSX -L products.xlsx -D ";"
```

This generates `examples/XLSX/CSV/products_Sheet1.csv`, with a log in `examples/XLSX/`.

**Delimiter behavior:** `-D` and the JSON setting `csv_delimiter` apply only to CSV output. Input CSV files are currently read using a comma separator.
