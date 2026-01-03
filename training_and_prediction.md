# Training and Prediction Guide

> **Reminder**  
> Version **1.0.0** only supports training models that use **EMA / state confirmation**.
> This guide assumes the full project is already set up and **all biosignal data has been uploaded to the Supabase SQL database**.

---

## Prerequisites

Before starting, ensure the following:

- Full project setup is complete. If not follow this [guide](initial_setup.md)
- Supabase database contains uploaded EmotiBit data. If not follow this [guide](data_upload.md)
- Python environment is available
- EmotiBit device is available for live prediction testing

---

## Project Structure

```
project-root/
├── .env
├── train_model/
│   ├── requirements.txt
│   ├── extract_data.py
│   ├── train_emotibit_model.py
│   ├── training_data/
│   └── models/
```

---

## Step 1: Environment Setup

1. Copy the `.env` file from the **GitHub root directory** into:

```
train_model/
```

2. Open a terminal in the `train_model` directory.

3. Install Python dependencies:

```bash
pip install -r requirements.txt
```

---

## Step 2: Extract Training Data

Download and prepare the training data from Supabase:

```bash
python extract_data.py
```

This step pulls biosignal data from the SQL database and formats it for training.

---

## Step 3: Train the Model

Once data extraction completes, train the model:

```bash
python train_emotibit_model.py
```

The trained model will be saved in:

```
train_model/models/
```

---

## Step 4: Live Prediction (LSL Streaming)

You can test real-time predictions using a live EmotiBit stream.

### Device Setup

1. Connect the EmotiBit to the **same WiFi network** as your computer.
2. Open **EmotiBit Oscilloscope**.
3. Enable:

```
Send data via: LSL
```

![EmotiBit Oscilloscope Screenshot](docs/images/lsl_stream.png)

### Start Live Prediction

With the LSL stream running, execute:

```bash
python train_emotibit_model.py
```

The script will now switch into **prediction mode**.

---

## Example Terminal Output

```text
[STATUS] now_lsl=112090.240 window=10.0s
ACC_X ->ax n=254 span=9.90s last_age=0.02s
ACC_Y ->ay n=254 span=9.90s last_age=0.02s
ACC_Z ->az n=254 span=9.90s last_age=0.02s
EDA ->eda n=150 span=9.90s last_age=0.02s
GYRO_X ->gyro_x n=254 span=9.90s last_age=0.02s
GYRO_Y ->gyro_y n=254 span=9.90s last_age=0.02s
GYRO_Z ->gyro_z n=254 span=9.90s last_age=0.02s
HR ->heart_rate n=13 span=8.40s last_age=0.32s
PPG_GRN ->ppg_green n=250 span=9.90s last_age=0.02s
TEMP1 ->temp n=75 span=9.80s last_age=0.11s
[23:53:45] -> walking (conf=0.62)
```

![EmotiBit Oscilloscope Screenshot](docs/images/prediction_stream.gif)

This output confirms:
- Sensors are correctly buffered
- Time windows are aligned
- Model predictions are being produced

---

## Interpreting Results

Use the output to:

- Identify sensors with insufficient data
- Decide whether to disable noisy signals
- Evaluate confidence levels for predictions

---

## Sample Dataset Testing

You can test a simplified activity model (sitting, standing, walking, running):

1. Clone the sample dataset:

```
https://github.com/geddie212/sample_data
```

2. Replace contents of:

```
train_model/training_data/
train_model/models/
```

3. Restart LSL streaming and rerun:

```bash
python train_emotibit_model.py
```

---


## Notes

- Training and prediction share the same pipeline
- Window-based batching ensures mixed-frequency signals are aligned
- EMA/state confirmation is required for valid predictions

---

