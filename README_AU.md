# BittyTax Australian 🇦🇺

**Cryptocurrency Tax Calculator for Australian Tax Rules**

A streamlined version of BittyTax adapted for Australian Taxation Office (ATO) requirements with a user-friendly graphical interface.

## 🚀 Quick Start (1-2 Minutes)

### 1. Setup
```bash
# Clone or download this repository
git clone <repository-url>
cd BittyTax

# Run the setup script
python setup_au.py
```

### 2. Launch
```bash
# Start the GUI application
python launch_bittytax_au.py

# Or use command line
python -m bittytax.bittytax sample_data/sample_transactions.csv
```

## 🇦🇺 Australian Features

### Tax Rules
- **Financial Year**: July 1 - June 30 (Australian FY)
- **Currency**: All calculations in AUD
- **CGT Discount**: 50% discount for assets held > 12 months
- **No Annual Allowance**: Unlike UK, Australia has no CGT-free allowance

### Supported Transaction Types
- **Trading**: Buy/sell cryptocurrency
- **Mining**: Mining rewards (taxed as income)
- **Staking**: Staking rewards (taxed as income)
- **Airdrops**: Airdrop receipts (taxed as income)
- **DeFi**: DeFi yield and liquidity mining

## 📊 Using the GUI

1. **Select File**: Choose your CSV/Excel transaction file
2. **Configure**: Set tax year and enable/disable CGT discount
3. **Calculate**: Click "Calculate Tax" and wait for processing
4. **Review**: Check results in the Summary, Holdings, and Tax Events tabs
5. **Export**: Save your tax report for ATO submission

## 🖥️ Command Line Interface (CLI)

For advanced users and testing purposes, you can also use the original BittyTax command-line tools directly. These provide more granular control and are useful for comparison with the GUI results.

### Conversion Tool (bittytax_conv)

Convert exchange/wallet files to BittyTax transaction format:

```bash
# Convert a single file to Excel format (default)
python -m bittytax.conv.bittytax_conv sample_data/sample_cro_tx.csv

# Convert to CSV format and output to terminal
python -m bittytax.conv.bittytax_conv --format CSV sample_data/sample_cro_tx.csv

# Convert with custom output filename
python -m bittytax.conv.bittytax_conv sample_data/sample_cro_tx.csv -o my_transactions.xlsx

# Convert multiple files at once
python -m bittytax.conv.bittytax_conv file1.csv file2.csv file3.xlsx

# Remove duplicate transactions across files
python -m bittytax.conv.bittytax_conv --duplicates *.csv

# Enable debug mode for troubleshooting
python -m bittytax.conv.bittytax_conv -d sample_data/sample_cro_tx.csv
```

### Tax Calculation Tool (bittytax)

Process transaction records and generate tax reports:

```bash
# Generate full tax report (PDF)
python -m bittytax.bittytax BittyTax_Records.xlsx

# Generate report for specific tax year
python -m bittytax.bittytax BittyTax_Records.xlsx -ty 2023

# Audit only (check balances without full tax calculation)
python -m bittytax.bittytax BittyTax_Records.xlsx --audit

# Output to terminal instead of PDF
python -m bittytax.bittytax BittyTax_Records.xlsx --nopdf

# Generate summary report for specific year
python -m bittytax.bittytax BittyTax_Records.xlsx --summary -ty 2023

# Enable debug mode for detailed processing logs
python -m bittytax.bittytax BittyTax_Records.xlsx -d

# Custom output filename
python -m bittytax.bittytax BittyTax_Records.xlsx -o MyTaxReport_2023.pdf
```

### Price Lookup Tool (bittytax_price)

Check current and historical cryptocurrency prices:

```bash
# Get latest price
python -m bittytax.price.bittytax_price latest BTC

# Get historical price
python -m bittytax.price.bittytax_price historic BTC 2023-01-15

# Calculate value for specific quantity
python -m bittytax.price.bittytax_price historic ETH 2023-06-15 0.5

# List all assets matching a symbol
python -m bittytax.price.bittytax_price list BTC

# Search for assets by name
python -m bittytax.price.bittytax_price list -s ethereum
```

### Quick Testing Pipeline

Combine conversion and tax calculation in one command:

```bash
# Convert and immediately audit balances
python -m bittytax.conv.bittytax_conv --format CSV sample_data/sample_cro_tx.csv | python -m bittytax.bittytax --audit --nopdf

# Convert and generate full tax report
python -m bittytax.conv.bittytax_conv sample_data/sample_cro_tx.csv -o temp_records.xlsx && python -m bittytax.bittytax temp_records.xlsx --nopdf
```

### CLI vs GUI Comparison

The CLI tools are useful for:
- **Batch processing** multiple files
- **Automation** and scripting
- **Debugging** with detailed logs
- **Testing** different configurations
- **Validation** of GUI results
- **Advanced users** who prefer command-line workflows

The GUI provides:
- **User-friendly** interface for non-technical users
- **Visual feedback** and error reporting
- **Australian-specific** settings and guidance
- **Integrated workflow** from file selection to report generation

### Notes for CLI Usage

1. **Module Import**: Always use `python -m bittytax.module.name` format to avoid import errors
2. **File Paths**: Use forward slashes `/` or escape backslashes `\\` in file paths
3. **Output Files**: CLI tools create files in the current working directory
4. **Debug Logs**: Use `-d` flag for detailed processing information
5. **Help**: Add `--help` to any command for full option details

## 📁 Transaction File Format

Your CSV file should have these columns:
```csv
Type,Buy Quantity,Buy Asset,Buy Value,Sell Quantity,Sell Asset,Sell Value,Fee Quantity,Fee Asset,Fee Value,Wallet,Timestamp,Note
Trade,1.0,BTC,50000.00,,,,,,,Coinbase,2023-01-15 10:30:00,Initial BTC purchase
Trade,,,,-0.2,BTC,12000.00,,,,,Coinbase,2023-12-10 16:45:00,Partial BTC sale
Mining,0.1,ETH,200.00,,,,,,,Mining Pool,2023-06-15 09:00:00,ETH mining reward
```

## 🔧 Manual Installation

If the setup script doesn't work:

```bash
# Install dependencies
pip install PyQt6 pandas matplotlib colorama tqdm requests pyyaml typing-extensions

# Run directly
python src/bittytax/ui_main.py
```

## 📋 Key Differences from UK Version

| Feature | UK Version | Australian Version |
|---------|------------|-------------------|
| Tax Year | April 6 - April 5 | July 1 - June 30 |
| Currency | GBP | AUD |
| CGT Allowance | £12,300 (2023) | None |
| CGT Discount | None | 50% for assets held > 12 months |
| CGT Rates | 10%/20% | Marginal income tax rates |

## 📋 Error Logging & Debugging

BittyTax Australian includes comprehensive error logging to help diagnose issues with transaction files and calculations.

### Error Log Location

All errors are automatically logged to:
```
~/.bittytax/logs/
├── bittytax_main.log      # General application logs
├── bittytax_conversion.log # File conversion errors
├── bittytax_tax.log       # Tax calculation errors
└── bittytax_ui.log        # User interface logs
```

### Viewing Error Details in the GUI

1. **Error Logs Tab**: Click the "Error Logs" tab to view:
   - Log file summary and sizes
   - Recent error messages
   - Detailed conversion errors with row-by-row analysis
   - Raw stderr output from the underlying BittyTax engine

2. **File Information Panel**: Select a file in the left panel to see:
   - Detailed analysis results
   - Parser recognition status
   - Specific error messages for unrecognised formats
   - Worksheet-by-worksheet breakdown for Excel files

3. **Conversion Status Tab**: Shows comprehensive file analysis:
   - Color-coded status indicators
   - Format recognition details
   - Error messages and warnings
   - Worksheet processing results

### Understanding Error Types

**Parser Failures**
```
Parser failure for "Coinbase Pro"
Row [15]: Invalid date format in timestamp column
```
- Indicates specific issues with data format
- Shows exact row numbers where problems occur
- Suggests which parser was attempted

**Format Recognition Issues**
```
File: transactions.csv - Status: Unrecognised - CSV format not recognised
```
- File structure doesn't match any known exchange format
- May need manual formatting or custom parser

**Data Validation Errors**
```
Row [23]: Missing required field 'Buy Quantity'
Row [45]: Invalid cryptocurrency symbol 'UNKNOWNCOIN'
```
- Specific data quality issues
- Row-level validation failures

### Detailed Error Capture

The application captures all underlying BittyTax error messages including:

- **File Processing**: Format detection and parser matching
- **Data Validation**: Row-by-row data quality checks
- **Conversion Errors**: Specific parsing failures with context
- **Tax Calculation**: Issues during tax event processing
- **Merge Operations**: Problems combining data from multiple sources

### Best Practices for Error Resolution

1. **Check the Error Logs Tab First**: Most issues are clearly explained there
2. **Review File Format**: Compare your file to the sample format
3. **Validate Data Quality**: Look for missing dates, amounts, or symbols
4. **Test with Sample Data**: Use the provided sample file to verify setup
5. **Enable Debug Mode**: For complex issues, check debug output in logs

### Common Error Patterns

**Date Format Issues**
```bash
# Correct format
2023-01-15 10:30:00

# Common mistakes
15/01/2023          # Wrong format
2023-1-15           # Missing zero padding
Jan 15, 2023        # Text format
```

**Missing Required Fields**
```bash
# Required columns for trades
Type,Buy Quantity,Buy Asset,Sell Quantity,Sell Asset,Timestamp

# Common mistakes
- Empty timestamp cells
- Missing asset symbols
- Zero quantities without corresponding sells
```

**Currency/Asset Symbol Issues**
```bash
# Correct
BTC, ETH, AUD

# Problematic
Bitcoin, Ethereum, AU$, $
```

## 🐛 Troubleshooting

### Common Issues

**"PyQt6 not found"**
```bash
pip install PyQt6
```

**"No module named bittytax"**
```bash
# Make sure you're in the right directory
cd BittyTax
python -c "import sys; sys.path.append('src'); import bittytax"
```

**"Calculation failed"**
- Check your CSV file format matches the example
- Ensure dates are in YYYY-MM-DD HH:MM:SS format
- Verify all required columns are present
- **Check the Error Logs tab for detailed diagnostics**

**"File format not recognised"**
- Review the detailed error information in the file info panel
- Compare your file structure to supported exchange formats
- Check for missing headers or incorrect column names
- Verify data encoding (should be UTF-8)

### Getting Help

1. **Check Error Logs Tab**: Most issues are explained in detail there
2. Check the sample data file: `sample_data/sample_transactions.csv`
3. Try the CLI version first: `python -m bittytax.bittytax --help`
4. Review log files in `~/.bittytax/logs/` for technical details
5. Enable debug mode in the GUI settings for verbose output

## ⚖️ Legal Disclaimer

This software is for informational purposes only and does not constitute tax advice. Always consult with a qualified tax professional or the ATO for official guidance on cryptocurrency taxation in Australia.

## 🔄 Updates from Original BittyTax

This is a focused adaptation of the original BittyTax project for Australian use. Key changes:

- **Simplified Setup**: One-command installation and launch
- **Australian Tax Rules**: ATO-compliant calculations
- **Modern UI**: PyQt6-based graphical interface
- **Local Use**: Optimized for desktop use, no deployment complexity

## 📞 Support

For Australian-specific tax questions, refer to:
- [ATO Cryptocurrency Guidance](https://www.ato.gov.au/individuals/investments-and-assets/crypto-asset-investments/)
- [ATO CGT Information](https://www.ato.gov.au/individuals/capital-gains-tax/)

---

**Ready to calculate your crypto taxes? Run `python setup_au.py` and get started in under 2 minutes!** 🚀 