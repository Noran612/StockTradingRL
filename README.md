
## StockTradingRL – An AI-Powered Stock Trading Agent

### Overview
**StockTradingRL** is a reinforcement learning project that trains an AI agent to make stock trading decisions using historical stock price data. The agent is trained to buy, sell, or hold based on patterns in past prices, aiming to maximize profit over time. This project includes a custom environment, `StocksEnvWithCapital`, which uses a specified number of past time periods (bars) to provide the agent with context when making trading decisions.

### Key Features
- **Customizable Historical Data Window**: `bars_count` allows you to define how many past data points the agent uses when deciding to buy, sell, or hold.
- **Validation Functions**: Track the agent’s performance and fine-tune parameters to optimize its trading strategy.
- **Save & Load Functionality**: Checkpoints allow for model saving, so you can continue training from a saved state.

### How It Works
1. **Environment Setup (`StocksEnvWithCapital`)**:
   - The environment represents stock trading actions in a simulation where the agent is exposed to historical prices.
   - Each state is made up of the last `bars_count` bars of price data, such as open, high, low, close prices, and volume.
   - The agent can take three actions: Buy, Sell (Close), and Skip (hold).
   - **Rewards** are calculated based on the profitability of trades, encouraging the agent to make decisions that yield higher returns.

2. **Training Loop**:
   - The agent explores different actions and uses feedback (rewards) to learn a policy for maximizing profits over time.
   - Periodic validation checks ensure the agent’s performance is on track.

### Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/StockTradingRL.git
   cd StockTradingRL
   ```

2. **Install Requirements**:
   This project requires Python 3.x and several libraries. Install them with:
   ```bash
   pip install -r requirements.txt
   ```
   The requirements may include:
   ```plaintext
   numpy
   torch
   gym
   ptan
   tensorboardX
   ```

### Usage

1. **Run Training**:
   The main training script (`train.py`) will train the agent using the `StocksEnvWithCapital` environment. You can adjust parameters like `bars_count`, learning rate, or training steps in the script or via command-line arguments.

   ```bash
   python train.py --data <path_to_data> --valdata <path_to_validation_data> --bars_count 10 --learning_rate 0.001
   ```

   Example:
   ```bash
   python train.py --data ./data/stock_data.csv --valdata ./data/validation_data.csv --bars_count 10 --learning_rate 0.001
   ```

2. **Validate Model**:
   Run a validation script to test the model’s performance. This is automatically done every `VALIDATION_EVERY_STEP` steps during training, but you can run it separately as well.

3. **Monitor Training with TensorBoard**:
   Training logs and validation statistics are saved in a format compatible with TensorBoard. To monitor:
   ```bash
   tensorboard --logdir=runs
   ```

4. **Modify `bars_count`**:
   Adjust the `bars_count` value in the training script to control how many past data points the agent uses to make decisions:
   ```python
   env = StocksEnvWithCapital(
       prices=stock_data, 
       bars_count=20,  # Use 20 bars of history instead of 10
       reset_on_close=True, 
       state_1d=True, 
       volumes=False
   )
   ```

### Project Structure

- **`train.py`**: Main training script where the agent learns through reinforcement learning.
- **`validation.py`**: Contains the `validation_run` function that evaluates the model’s performance.
- **`env/StocksEnvWithCapital.py`**: Custom environment class defining the stock trading simulation.
- **`data/`**: Folder for training and validation data files.

### Future Improvements
Some possible next steps for development:
- **Enhance Reward Calculation**: Adjust rewards for more complex trading strategies, such as considering risk-adjusted returns.
- **Add More Technical Indicators**: Use additional features like moving averages, relative strength index (RSI), or volume analysis.
- **Integrate Live Data**: With minor modifications, this setup could be adapted to trade on live market data.



