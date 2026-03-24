# Test Procedure — PLC Batch Process with Recipe Management

## 1. Objective

This test procedure verifies that the PLC batch process operates correctly, including recipe loading, sequencing, process simulation, and system reset behavior.

---

## 2. Test Environment

* Platform: Studio 5000 Logix Designer
* Mode: Emulator or offline simulation
* Inputs manually controlled via tags

---

## 3. Tags to Monitor (Watch Window)

### Recipe & Control

* Recipe_Select
* Active_Fill1_SP
* Active_Fill2_SP
* Active_Fill3_SP
* Active_MixTime_SP
* Active_Temp_SP

### Steps

* Step_Idle
* Step_LoadRecipe
* Step_Fill1
* Step_Fill2
* Step_Fill3
* Step_Heat
* Step_Mix
* Step_Complete

### Process Values

* Fill1_Total
* Fill2_Total
* Fill3_Total
* Tank_Level
* Temp_PV

### Outputs

* Valve_1
* Valve_2
* Valve_3
* Heat_Enable
* Mixer_Motor
* Batch_Complete_Light

---

## 4. Test Procedures

---

### Test 1 — Recipe Loading

**Steps:**

1. Set Recipe_Select = 1
2. Press PB_Start

**Expected Results:**

* Active setpoints match Recipe 1 values
* Recipe_Loaded bit turns on
* Step transitions to Fill1

Repeat for Recipe 2 and Recipe 3.

---

### Test 2 — Ingredient Fill Sequence

**Steps:**

1. Start a batch
2. Observe valve outputs and totals

**Expected Results:**

* Valve_1 opens first until Fill1_Total reaches setpoint
* Valve_2 opens after Fill1 completes
* Valve_3 opens after Fill2 completes
* Only one valve runs at a time

---

### Test 3 — Tank Level Calculation

**Steps:**

1. Allow all fills to complete
2. Observe Tank_Level

**Expected Results:**

* Tank_Level equals Fill1_Total + Fill2_Total + Fill3_Total

---

### Test 4 — Heating Stage

**Steps:**

1. Allow fill steps to complete
2. Observe heating behavior

**Expected Results:**

* Heat_Enable turns on
* Temp_PV increases over time
* Temp_Ready becomes true when Temp_PV ≥ Active_Temp_SP

---

### Test 5 — Mixing Stage

**Steps:**

1. Allow system to reach mix step
2. Observe mixer and timer

**Expected Results:**

* Mixer_Motor turns on
* T_Mix runs for Active_MixTime_SP
* Mix_Done turns true when timer finishes

---

### Test 6 — Batch Completion

**Steps:**

1. Allow full sequence to finish

**Expected Results:**

* Step_Complete turns on
* Batch_Complete_Light turns on
* Batch_Active turns off

---

### Test 7 — Reset Function

**Steps:**

1. Press PB_Reset

**Expected Results:**

* All step bits turn off
* All totals reset to 0
* Temp_PV resets to initial value
* Timers reset
* System_Run turns off

---

## 5. Pass Criteria

The system is considered functional if:

* Recipe values load correctly for all selections
* Sequence follows the correct order
* Process values update accurately
* Mixer and heater operate at correct times
* Batch completes without errors
* Reset returns system to a clean state

---

## 6. Notes

* Use slower timer presets if debugging is needed
* Verify one-shot logic prevents repeated triggers
* Confirm Recipe_Select stays within valid range (1–3)

---

## 7. Conclusion

This test procedure confirms that the PLC logic correctly implements a recipe-driven batch process with sequential control, simulated process variables, and reliable system reset behavior.
