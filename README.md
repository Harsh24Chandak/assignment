# Option Chain Data using Upstox API

## Option Chain Margin and Premium Calculator

## Overview
This project provides a streamlined solution to retrieve option chain data and calculate the margin required and premium earned for specific options contracts. The two main functions in this project help traders quickly assess both the cost and potential earnings from options contracts for NIFTY or BANKNIFTY, using real-time data.

## Code Structure and Function Logic

### Part 1: `get_option_chain_data`
**Objective**: Fetch the option chain data for a specified instrument and expiry date, selecting either the highest bid price for put options or the highest ask price for call options at each strike price.

#### Function Inputs:
- `instrument_name`: Name of the instrument (e.g., NIFTY or BANKNIFTY).
- `expiry_date`: Expiry date of the options in YYYY-MM-DD format.
- `side`: Type of option to retrieve; "PE" for Put or "CE" for Call.

#### Function Logic:
1. **API Call**: The function retrieves the option chain data from the broker’s API.
2. **Filtering**: For each strike price, it checks the side parameter:
   - If `side == "PE"`, it selects the highest bid price.
   - If `side == "CE"`, it selects the highest ask price.
3. **Data Structuring**: The function organizes the data into a DataFrame with columns:
   - `instrument_name`, `strike_price`, `side`, and `bid/ask`.

#### Example Output:
| instrument_name | strike_price | side | bid/ask |
|-----------------|--------------|------|---------|
| NIFTY           | 19500        | PE   | 0.65    |
| NIFTY           | 19500        | CE   | 2302.25 |

---

### Part 2: `calculate_margin_and_premium`
**Objective**: Extend the DataFrame from `get_option_chain_data` with two additional columns: `margin_required` and `premium_earned`.

#### Function Inputs:
- `data`: The DataFrame returned by `get_option_chain_data`.

#### Function Logic:
1. **Margin Calculation**:
   - The function calls the broker’s API to retrieve the margin required for each option contract with a "Sell" transaction type.
2. **Premium Calculation**:
   - Multiplies the bid or ask price by the `lot_size` for each option to calculate the premium earned.

#### Output:
The function returns a modified DataFrame with two additional columns:
- `margin_required`: The margin required to sell the option.
- `premium_earned`: The calculated premium earned from selling the option.

#### Example Output:
| instrument_name | strike_price | side | bid/ask | margin_required | premium_earned |
|-----------------|--------------|------|---------|-----------------|----------------|
| NIFTY           | 19500        | PE   | 0.65    | 1950           | 780            |

---

## Approach and Considerations
1. **Efficiency**: Leveraged efficient DataFrame operations to handle potentially large datasets.
2. **Scalability**: Structured the code to handle various instruments and expiry dates, making it adaptable for other trading strategies.
3. **Error Handling**: Added basic error handling for API connectivity and missing data. Future enhancements could improve error handling further for smoother runtime in dynamic market conditions.

## AI Tools Used
I used **ChatGPT** to accelerate development in the following ways:
- **Code Structure Guidance**: ChatGPT assisted in generating a function skeleton for data retrieval, helping me organize inputs and outputs logically.
- **Logic Refinement**: I utilized ChatGPT for debugging syntax errors and understanding API integration.
- **Documentation Support**: ChatGPT provided suggestions on how to clearly explain each function’s purpose and approach, improving the clarity of this README.

## Future Enhancements
1. **Additional Metrics**: Expanding the function to calculate additional financial metrics like delta, theta, and vega for comprehensive analysis.
2. **Enhanced Error Handling**: Improving robustness for API response errors or handling market fluctuations.
3. **User Interface**: Developing a simple user interface to make it easier for traders to interact with the tool.

## Conclusion
This project offers a practical solution to assess the risk and profitability of options contracts. The code structure and use of API integration provide essential metrics for informed trading decisions. By using AI tools, I streamlined development, ensuring clarity and robustness in the final solution.
