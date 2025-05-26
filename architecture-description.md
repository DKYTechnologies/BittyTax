# BittyTax Architecture Description

## Overview
BittyTax is a Python-based cryptocurrency tax calculation tool specifically designed for UK tax rules. The project consists of three main command-line tools and follows a modular architecture pattern. This document describes the system's architecture, components, and their interactions.

## System Components

### 1. Core Tools
The system is divided into three main command-line tools:

1. **BittyTax (`bittytax`)**: The main accounting tool that processes transaction records and generates tax reports
2. **Conversion Tool (`bittytax_conv`)**: Converts wallet and exchange data into standardized transaction records
3. **Price Tool (`bittytax_price`)**: Handles historic price data lookups for cryptocurrencies and foreign currencies

### 2. Project Structure

```
BittyTax/
├── src/bittytax/           # Main package directory
│   ├── conv/              # Conversion tool implementation
│   │   └── mergers/      # Data merging modules for various exchanges/sources
│   │       ├── binance.py     # Merges Binance staking & trading data
│   │       ├── coincorner.py  # Handles CoinCorner trade consolidation
│   │       ├── etherscan.py   # Processes Ethereum blockchain transactions
│   │       └── snowtrace.py   # Handles Avalanche blockchain data
│   ├── price/            # Price lookup tool implementation
│   ├── config/           # Configuration management
│   ├── templates/        # Report templates
│   ├── bittytax.py      # Main entry point
│   ├── tax.py           # Tax calculation core
│   ├── transactions.py   # Transaction processing
│   └── report.py        # Report generation
├── scripts/              # Utility scripts
│   ├── batch/           # Windows batch scripts for common operations
│   │   ├── BittyTax Accounting Tool.bat    # Drag-and-drop accounting interface
│   │   ├── BittyTax Audit Tool.bat         # Drag-and-drop auditing
│   │   ├── BittyTax Config.bat             # Configuration editor
│   │   ├── BittyTax Conversion Tool.bat    # Data conversion interface
│   │   └── BittyTax Install/Update.bat     # Installation scripts
│   └── powershell/      # PowerShell GUI implementations
│       ├── BittyTax Accounting Tool.ps1    # GUI for accounting operations
│       └── BittyTax Conversion Tool.ps1    # GUI for data conversion
├── data/                 # Example data and resources
└── tests/               # Test suite
```

### 3. Core Components

#### 3.1 Transaction Processing (`transactions.py`, `t_record.py`, `t_row.py`)
- Handles parsing and validation of transaction records
- Manages transaction data structures and transformations
- Implements transaction type-specific logic

#### 3.2 Tax Calculation Engine (`tax.py`, `tax_event.py`)
- Implements UK tax calculation rules
- Processes capital gains calculations
- Handles income tax calculations
- Manages tax year specific rules

#### 3.3 Report Generation (`report.py`, `audit.py`, `audit_excel.py`)
- Generates PDF tax reports
- Produces audit trails
- Creates Excel-based reports
- Implements various report templates

#### 3.4 Price Management (`price/`)
- Interfaces with price data sources
- Handles historical price lookups
- Manages currency conversions

#### 3.5 Data Conversion (`conv/`)
- Implements various exchange and wallet format parsers
- Standardizes transaction data
- Provides data validation and cleaning
- Contains merger modules for consolidating data from specific sources:
  - Binance merger: Handles staking operations and Liquid Swap transactions
  - CoinCorner merger: Consolidates same-timestamp trades
  - Etherscan merger: Processes complex blockchain transactions and fees
  - Snowtrace merger: Manages Avalanche blockchain data using Etherscan patterns

#### 3.6 Configuration Management (`config/`, `config.py`)
- Manages system configuration
- Handles user preferences
- Implements configuration validation

### 4. Dependencies

The system relies on several key external dependencies:
- Data Processing: `pandas`, `openpyxl`, `xlrd`, `xlsxwriter`
- Report Generation: `xhtml2pdf`, `jinja2`
- Network Operations: `requests`
- Data Formats: `pyyaml`, `defusedxml`
- Development Tools: `black`, `flake8`, `pylint`, `mypy`

### 5. Data Flow

1. **Input Processing**
   - Raw data from various sources
   - Conversion to standardized format
   - Validation and normalization

2. **Tax Calculation**
   - Transaction sorting and categorization
   - Application of tax rules
   - Capital gains computation
   - Income calculation

3. **Report Generation**
   - Data aggregation
   - Template rendering
   - PDF/Excel generation
   - Audit trail creation

### 6. Extension Points

The system is designed to be extensible in several areas:
- New exchange/wallet format parsers
- Additional price data sources
- Custom report templates
- Tax rule modifications
- New transaction types

### 7. Security Considerations

- Local data processing (no external data sharing)
- Input validation and sanitization
- Secure price data retrieval
- Configuration file protection
- API key management

### 8. Performance Considerations

- Efficient transaction processing
- Optimized price data caching
- Minimal memory footprint
- Parallel processing where applicable

### 9. User Interface Tools

The system provides two types of user interface tools:

1. **Batch Scripts** (`scripts/batch/`)
   - Simple drag-and-drop interfaces for common operations
   - Configuration management utilities
   - Installation and update scripts
   - Direct access to core functionality without command line knowledge

2. **PowerShell GUI** (`scripts/powershell/`)
   - Sophisticated graphical interfaces for main operations
   - File selection dialogs and argument input forms
   - Success notifications and report access
   - Enhanced user experience for Windows users

These tools make BittyTax accessible to users who prefer not to use the command line interface directly.

## Development Guidelines

1. **Code Style**
   - Follows PEP 8 guidelines
   - Uses type hints (Python 3.7+)
   - Implements comprehensive error handling
   - Includes detailed documentation

2. **Testing**
   - Unit tests for core components
   - Integration tests for tools
   - HMRC example test cases
   - Performance benchmarks

3. **Documentation**
   - Inline code documentation
   - API documentation
   - User guides
   - Example implementations

## Future Considerations

1. **Scalability**
   - Support for larger transaction volumes
   - Additional data source integrations
   - Enhanced reporting capabilities
   - International tax rule support

2. **Maintenance**
   - Regular updates for tax rule changes
   - Price source maintenance
   - Dependency updates
   - Security patches
