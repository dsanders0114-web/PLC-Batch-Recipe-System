# PLC Batch Process with Recipe Management (Studio 5000)

## Overview

This project simulates a batch mixing process using Studio 5000 ladder logic. The system models a mixing tank with three ingredient valves, a heating stage, and a mixer motor.

The main focus of the project is recipe management. An operator selects a recipe, and the PLC automatically loads all required process parameters and runs the batch sequence from start to finish.

---

## Key Features

* Recipe selection using integer input (3 products)
* Automatic loading of recipe parameters from arrays
* Sequential batch process control:

  * Ingredient 1 fill
  * Ingredient 2 fill
  * Ingredient 3 fill
  * Heating to temperature setpoint
  * Mixing for defined time
* Simulated process values (tank level and temperature)
* One-shot logic for clean event control
* Timer-based process simulation
* Reset logic for full system recovery

---

## How the System Works

### 1. Recipe Selection

The operator selects a recipe:

* 1 = Product A
* 2 = Product B
* 3 = Product C

Each recipe includes:

* Ingredient fill targets
* Mix time
* Temperature setpoint

These values are stored in arrays and loaded into active process tags when the batch starts.

---

### 2. Batch Sequence

The PLC runs the process in the following order:

1. Idle (waiting for start)
2. Load selected recipe
3. Fill Ingredient 1
4. Fill Ingredient 2
5. Fill Ingredient 3
6. Heat to temperature setpoint
7. Mix for recipe-defined time
8. Batch complete

Each step must finish before the next begins.

---

### 3. Process Simulation

* Ingredient flow is simulated using timers that increment totals
* Tank level is calculated from all ingredient totals
* Temperature rises gradually while heating is enabled
* Mixer runs for the exact time defined by the recipe

---

## Technologies Used

* Studio 5000 Logix Designer
* Ladder Logic
* Arrays for recipe storage
* Timers (TON)
* Compare and math instructions (GEQ, ADD, MOV)

---

## Files Included

* `.ACD` file (full PLC project)
* `.L5X` file (exported logic for review)
* `test_procedure.md` (validation steps)
* screenshots of ladder logic and system behavior

---

## Key Learning Outcomes

* Building a structured batch sequence using step logic
* Implementing recipe management using arrays
* Synchronizing process variables with control logic
* Using timers to simulate real-world processes
* Designing logic that scales across multiple products



---

## Author

Daryl Sanders


