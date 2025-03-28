# WiFiPumpkin Python 3 Modernization

This repository contains a fork of [WiFiPumpkin](https://github.com/my0aung/wifipumpkin) with the goal of modernizing the codebase to work with Python 3.

## Background

WiFiPumpkin was originally written for Python 2, which reached its end of life on January 1, 2020. This project aims to update the codebase to be compatible with Python 3 while maintaining all functionality.

## Modernization Process

There are several methods to convert Python 2 code to Python 3. This guide outlines the steps to modernize the WiFiPumpkin codebase.

### Method 1: Using 2to3 Tool

The `2to3` tool is included with Python 3 and automates much of the conversion process.

1. Clone the repository:
   ```bash
   git clone https://github.com/tonyakaguwop/wifipumpkin.git
   cd wifipumpkin
   ```

2. Install the required package if missing:
   ```bash
   sudo apt-get install python3-lib2to3
   ```

3. Run the conversion tool:
   ```bash
   2to3 -w .
   ```
   The `-w` flag writes changes directly to the files instead of just showing the diffs.

### Method 2: Using Modernize

The `modernize` tool is an enhanced version of `2to3` that produces more idiomatic Python 3 code that's also compatible with Python 2.

1. Create a virtual environment to avoid permission issues:
   ```bash
   python3 -m venv ~/wifipumpkin_env
   source ~/wifipumpkin_env/bin/activate
   ```

2. Install modernize:
   ```bash
   pip install modernize
   ```

3. Run modernize:
   ```bash
   python -m libmodernize -w .
   ```

### Method 3: Using pipx (Alternative)

If you prefer not to create a virtual environment:

1. Install pipx:
   ```bash
   sudo apt install pipx
   ```

2. Run modernize with pipx:
   ```bash
   pipx run modernize -w .
   ```

## Post-Conversion Steps

After running the automated conversion tools, manual intervention is likely needed:

1. Fix imports:
   - Update deprecated module imports
   - Handle renamed modules (e.g., `Queue` to `queue`)

2. Address string/bytes issues:
   - Python 3 distinguishes between strings (Unicode) and bytes
   - Fix string encoding/decoding issues

3. Update iterator methods:
   - Replace `.iteritems()`, `.iterkeys()`, `.itervalues()` with `.items()`, `.keys()`, `.values()`

4. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

5. Test functionality:
   - Run unit tests if available
   - Test main features to verify they work as expected

## Common Issues and Fixes

### Print Statements
- Python 2: `print "Hello"`
- Python 3: `print("Hello")`

### Unicode Handling
- Python 2: Uses ASCII strings by default
- Python 3: Uses Unicode strings by default

### Division Operator
- Python 2: Integer division by default (`5 / 2 = 2`)
- Python 3: Float division by default (`5 / 2 = 2.5`)

### Exception Syntax
- Python 2: `except Exception, e:`
- Python 3: `except Exception as e:`

### Range vs xrange
- Python 2: Both `range()` and `xrange()`
- Python 3: Only `range()` (behaves like the old `xrange()`)

## Contributing

Contributions to improve the Python 3 compatibility are welcome:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## Known Limitations

- Some external dependencies may still require Python 2
- Network interface handling might differ between Python 2 and 3
- Some third-party libraries used by WiFiPumpkin might not be compatible with Python 3

## License

This project maintains the same license as the original WiFiPumpkin repository.
