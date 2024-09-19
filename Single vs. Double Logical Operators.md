### Understanding Single vs. Double Logical Operators (`&` vs. `&&`, `|` vs. `||`)

When coding in MATLAB, logical operators are essential for evaluating expressions to determine whether they are **true** or **false**. This distinction allows for decision-making in programming, which is crucial when writing conditional statements or loops. MATLAB has both **element-wise** logical operators (single `&`, `|`) and **short-circuit** logical operators (double `&&`, `||`).

The two main categories of logical operators for **AND** and **OR** conditions are:
1. **Single Logical AND (`&`)** and **Single Logical OR (`|`)**
2. **Double Logical AND (`&&`)** and **Double Logical OR (`||`)**

### Key Concepts to Know

#### 1. **Logical Operations**:
A **logical operation** compares two values or conditions and returns **true** or **false**:
- **True (1)**: When a condition is satisfied.
- **False (0)**: When a condition is not satisfied.

#### 2. **Conditions and Expressions**:
A **condition** is an expression that evaluates whether something is true or false. For example:
- `power(1) > threshold`: This checks whether the first power value is greater than a threshold.

#### 3. **Scalars and Vectors**:
- A **scalar** is a single value (e.g., `5`).
- A **vector** is a list of values (e.g., `[1, 2, 3]`). In MATLAB, these values are stored in arrays.

#### 4. **Element-wise Operations**:
This refers to operations performed on each element of a vector or array, one at a time. For example, with two vectors of power values from two electrodes, an element-wise operation compares or operates on the power values at each time point across the electrodes.

---

### Single AND (`&`) and Single OR (`|`) - Element-Wise Logical Operators

- **What is it?**: The single `&` (AND) and `|` (OR) operators compare two arrays **element by element** and check if the condition is true for each pair of elements.
- **When to use it**: Use these when you want to compare arrays or vectors element by element.
  
#### Example of Single AND (`&`): Time-Frequency Analysis
```matlab
% Simulated power values (in µV^2) across frequencies (rows) and electrodes (columns)
power_electrode1 = [5, 7, 10, 6];  % Power values at 4 different frequencies (e.g., 5Hz, 10Hz, etc.)
power_electrode2 = [6, 3, 12, 5];  % Power values for another electrode

% Check if both electrodes have power > 5 µV^2 at each frequency
result = (power_electrode1 > 5) & (power_electrode2 > 5);
% result = [false, false, true, false]
```
- **Explanation**:
  - `power_electrode1 > 5` evaluates to `[false, true, true, true]`.
  - `power_electrode2 > 5` evaluates to `[true, false, true, false]`.
  - Using `&`, MATLAB checks each element and returns `[false, false, true, false]`.

#### Example of Single OR (`|`): Behavioral Accuracy and Reaction Time
```matlab
% Simulated behavioral accuracy (1 = correct, 0 = incorrect) and reaction times in ms
accuracy = [1, 0, 1, 1];  
reaction_times = [480, 530, 450, 610];  % Reaction times in milliseconds

% Check if participants were either correct or responded fast (< 500 ms)
result = (accuracy == 1) | (reaction_times < 500);
% result = [true, false, true, true]
```
- **Explanation**:
  - `accuracy == 1` evaluates to `[true, false, true, true]`.
  - `reaction_times < 500` evaluates to `[true, false, true, false]`.
  - Using `|`, MATLAB checks if either condition is true element by element, resulting in `[true, false, true, true]`.

---

### Double AND (`&&`) and Double OR (`||`) - Short-Circuit Logical Operators

- **What is it?**: The double `&&` (AND) and `||` (OR) operators are used with **scalars** or single logical conditions. They short-circuit, meaning if the first condition is false, MATLAB stops evaluating the rest of the conditions.
- **When to use it**: Use these when comparing single values (scalars) or when you want to save time by not evaluating further conditions if the first is false.

#### Example of Double AND (`&&`): Checking Overall Trial Performance
```matlab
% Check if a participant was both fast and correct in a single trial
reaction_time_trial = 490;  % Reaction time in milliseconds
accuracy_trial = 1;  % 1 = correct, 0 = incorrect

% Check if the participant was fast (< 500 ms) and correct
if (reaction_time_trial < 500) && (accuracy_trial == 1)
    disp('The participant was both fast and correct.');
end
```
- **Explanation**:
  - MATLAB first checks `reaction_time_trial < 500` (true).
  - Then it checks `accuracy_trial == 1` (true).
  - Since both conditions are true, the result is true, and MATLAB runs the `disp` command.

#### Example of Double OR (`||`): Time-Frequency Analysis
```matlab
% Power values at 10Hz and 15Hz for a single electrode
power_at_10Hz = 8;  % µV^2 at 10Hz
power_at_15Hz = 12;  % µV^2 at 15Hz

% Check if power at 10Hz or 15Hz exceeds a threshold (e.g., 10 µV^2)
if (power_at_10Hz > 10) || (power_at_15Hz > 10)
    disp('Significant power at either 10Hz or 15Hz.');
end
```
- **Explanation**:
  - MATLAB checks `power_at_10Hz > 10` (false).
  - Then it checks `power_at_15Hz > 10` (true).
  - The result is true since one of the conditions is true, so the `disp` command runs.

---
### How to Decide Which to Use:

1. **Use `&` or `|`** when:
   - You are working with arrays or vectors.
   - You need to compare multiple elements at once, element by element.

   **Example**: Comparing EEG power across electrodes.
   ```matlab
   power_electrode1 = [5, 7, 10];
   power_electrode2 = [4, 6, 11];
   result = (power_electrode1 > 6) & (power_electrode2 > 6);
   % result = [false, true, true]
   ```

2. **Use `&&` or `||`** when:
   - You are working with single logical conditions (scalars).
   - You want to save time by stopping the evaluation if the first condition is false (short-circuiting).

   **Example**: Analyzing trial performance.
   ```matlab
   reaction_time = 520;
   accuracy = 1;
   if (reaction_time < 500) && (accuracy == 1)
       disp('Fast and correct trial');
   end
   ```
