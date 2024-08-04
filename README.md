# 🎨 Calculator Project 🎨

Welcome to the Calculator Project repository! This project is a simple yet functional calculator built using modern web technologies.

## Table of Contents

1. [About](#about)
2. [Features](#features)
3. [Technologies Used](#technologies-used)
4. [Installation](#installation)
5. [Usage](#usage)
6. [Project Structure](#project-structure)
7. [Contributing](#contributing)
8. [License](#license)
9. [Contact](#contact)

## About

✨ This calculator project aims to provide a basic, user-friendly tool for performing arithmetic operations. It's a great project for beginners to practice HTML, CSS, and JavaScript, and for others to use as a quick, on-the-go calculator.

## Features

✔️ Simple and intuitive user interface  
✔️ Basic arithmetic operations: addition, subtraction, multiplication, division  
✔️ Clear button to reset the calculator  
✔️ Responsive design for all device sizes

## Technologies Used

- **Frontend:**
  - 🌐 HTML5
  - 🎨 CSS3
  - ⚙️ JavaScript (ES6+)

## Installation

To run this project locally, follow these steps:

1. **Clone the repository:**

    ```bash
    git clone https://github.com/yourusername/calculator-project.git
    cd calculator-project
    ```

2. **Open the index.html file in your browser:**

    ```bash
    open index.html
    ```

## Usage

🖱️ **Calculator Interface:**  
- Click the buttons to input numbers and operators.
- Click the `=` button to calculate the result.
- Click the `C` button to clear the input.

## Project Structure

```
calculator-project/
├── css/
│   └── styles.css
├── js/
│   └── script.js
├── index.html
└── README.md
```

## Contributing

🌟 Contributions are welcome! Please follow these steps:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes.
4. Commit your changes (`git commit -m 'Add some feature'`).
5. Push to the branch (`git push origin feature-branch`).
6. Open a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

📧 For any inquiries, please contact [your-email@example.com](mailto:your-email@example.com).

---

Feel free to customize this template according to your project's specifics and needs. Enjoy coding! 🎉

---

Here's a simple example of what the files might contain:

**index.html:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <link rel="stylesheet" href="css/styles.css">
</head>
<body>
    <div class="calculator">
        <input type="text" class="calculator-screen" value="" disabled />
        <div class="calculator-keys">
            <button type="button" class="operator" value="+">+</button>
            <button type="button" class="operator" value="-">-</button>
            <button type="button" class="operator" value="*">*</button>
            <button type="button" class="operator" value="/">/</button>
            <button type="button" value="7">7</button>
            <button type="button" value="8">8</button>
            <button type="button" value="9">9</button>
            <button type="button" value="4">4</button>
            <button type="button" value="5">5</button>
            <button type="button" value="6">6</button>
            <button type="button" value="1">1</button>
            <button type="button" value="2">2</button>
            <button type="button" value="3">3</button>
            <button type="button" value="0">0</button>
            <button type="button" class="decimal" value=".">.</button>
            <button type="button" class="all-clear" value="all-clear">C</button>
            <button type="button" class="equal-sign operator" value="=">=</button>
        </div>
    </div>
    <script src="js/script.js"></script>
</body>
</html>
```

**css/styles.css:**
```css
body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f7f7f7;
    font-family: 'Arial', sans-serif;
}

.calculator {
    border: 1px solid #ccc;
    border-radius: 5px;
    width: 300px;
}

.calculator-screen {
    width: 100%;
    height: 80px;
    border: none;
    background-color: #252525;
    color: white;
    font-size: 2.5rem;
    text-align: right;
    padding: 10px;
    box-sizing: border-box;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
}

.calculator-keys {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
}

button {
    height: 80px;
    font-size: 1.5rem;
    border: 1px solid #ccc;
    background-color: white;
    cursor: pointer;
}

button.operator {
    background-color: #f59e0b;
    color: white;
}

button.all-clear {
    background-color: #f43f5e;
    color: white;
    grid-column: span 2;
}

button.equal-sign {
    background-color: #10b981;
    color: white;
    grid-column: span 2;
}

button:hover {
    opacity: 0.8;
}
```

**js/script.js:**
```javascript
const calculator = {
    displayValue: '0',
    firstOperand: null,
    waitingForSecondOperand: false,
    operator: null,
};

function inputDigit(digit) {
    const { displayValue, waitingForSecondOperand } = calculator;

    if (waitingForSecondOperand === true) {
        calculator.displayValue = digit;
        calculator.waitingForSecondOperand = false;
    } else {
        calculator.displayValue = displayValue === '0' ? digit : displayValue + digit;
    }
}

function inputDecimal(dot) {
    if (calculator.waitingForSecondOperand === true) {
        calculator.displayValue = '0.'
        calculator.waitingForSecondOperand = false;
        return
    }

    if (!calculator.displayValue.includes(dot)) {
        calculator.displayValue += dot;
    }
}

function handleOperator(nextOperator) {
    const { firstOperand, displayValue, operator } = calculator
    const inputValue = parseFloat(displayValue);

    if (operator && calculator.waitingForSecondOperand)  {
        calculator.operator = nextOperator;
        return;
    }

    if (firstOperand == null) {
        calculator.firstOperand = inputValue;
    } else if (operator) {
        const currentValue = firstOperand || 0;
        const result = performCalculation[operator](currentValue, inputValue);

        calculator.displayValue = String(result);
        calculator.firstOperand = result;
    }

    calculator.waitingForSecondOperand = true;
    calculator.operator = nextOperator;
}

const performCalculation = {
    '/': (firstOperand, secondOperand) => firstOperand / secondOperand,
    '*': (firstOperand, secondOperand) => firstOperand * secondOperand,
    '+': (firstOperand, secondOperand) => firstOperand + secondOperand,
    '-': (firstOperand, secondOperand) => firstOperand - secondOperand,
    '=': (firstOperand, secondOperand) => secondOperand
};

function resetCalculator() {
    calculator.displayValue = '0';
    calculator.firstOperand = null;
    calculator.waitingForSecondOperand = false;
    calculator.operator = null;
}

function updateDisplay() {
    const display = document.querySelector('.calculator-screen');
    display.value = calculator.displayValue;
}

updateDisplay();

const keys = document.querySelector('.calculator-keys');
keys.addEventListener('click', (event) => {
    const { target } = event;
    const { value } = target;
    if (!target.matches('button')) {
        return;
    }

    switch (value) {
        case '+':
        case '-':
        case '*':
        case '/':
        case '=':
            handleOperator(value);
            break;
        case '.':
            inputDecimal(value);
            break;
        case 'all-clear':
            resetCalculator();
            break;
        default:
            if (Number.isInteger(parseFloat(value))) {
                inputDigit(value);
            }
    }

    updateDisplay();
});
```

Feel free to modify and enhance this template according to your project's requirements. Enjoy coding! 🎉
