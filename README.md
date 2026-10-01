# Neural Networks and Google Stock Price Prediction

Neural network project using TensorFlow/Keras and LSTM-based prediction of Google stock prices.

## Contents

- `neural_networks.ipynb`:Notebook with exercises, explanations, code comments, and chart labels. 
- `GOOG.csv`: 1,259 observations from December 7, 2015 to December 4, 2020. Columns: Date, Open, High, Low, Close, Adj Close, and Volume.
- `requirements.txt`: Python dependencies identified in the notebook; this is not a validated environment specification.
- `.gitignore`: excludes virtual environments, caches, logs, and training outputs.

The notebook covers linear and logistic regression, dense neural networks, California Housing, direct TensorFlow model implementations, Fashion MNIST, hyperparameter search, and LSTM time-series prediction.

## Getting started

From the project directory, create a virtual environment and install the dependencies:

```bash
python -m venv .venv
# Linux / macOS:
source .venv/bin/activate
# Windows PowerShell:
# .venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
jupyter lab neural_networks.ipynb
```

Keep `GOOG.csv` in the same directory as the notebook. It is loaded using a relative path.

## Reproducibility and compatibility

The exercise template dates from 2020 and needs adaptation before a complete run in a current environment:

- The notebook clones [the original exercise repository](https://github.com/luisferuam/MIAX5) and uses its `dlfbt` module, predefined California Housing weights, and test fixtures. Those resources are not bundled here.
- Check compatibility with the historical weights when adapting the notebook.
- It includes the Colab-specific `%tensorflow_version 2.x` command, in-cell package installations, and shell commands. Review those cells before running locally.
- It uses the historical `kerastuner` import, mixes Keras and TensorFlow imports, and contains historical TensorBoard.dev commands and links. Review compatibility with the installed versions.
- The code cell containing a bare TensorBoard URL must be converted to Markdown or a comment before execution.
- Some cells delete local log and hyperparameter-search directories before starting new runs.
- California Housing and Fashion MNIST require data downloads when not cached locally.
- The hyperparameter sweep with cross-validation can take substantial time.
- The 5-fold training function constructs an optimizer with a selected learning rate but passes its string name to `compile()`, so the configured learning rate is not applied there.

## LSTM experiment limitations

The experiment uses windows of 60 trading sessions and a chronological split with the first 800 observations for training. Review the following before interpreting results:

- `MinMaxScaler` is fitted again with `fit_transform(test_2)`, using information from the evaluation period and a different scale. Fit the scaler on training data only, then use `transform` on validation and test data.
- Hyperparameter selection uses the set called test for validation. Reserve an independent final test set and use temporal validation.
- Some sizes and indices are hard-coded. The variable `nepochs` is reused as a plotting range and subsequently passed as a training argument.
- No independent final evaluation against a simple baseline, such as the previous closing price, is provided. The original visual conclusions do not establish out-of-sample predictive ability.
