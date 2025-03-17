# Face Swapping Using SAEHD Model

## Setup Instructions

### 1. Create a Virtual Environment
Ensure you have Python 3.8 installed on your system. Then, create and activate a virtual environment:

```sh
python -m venv venv
source venv/bin/activate  # For macOS/Linux
venv\Scripts\activate  # For Windows
```

### 2. Install Dependencies
Install the required packages using `requirements_cuda.txt`:

```sh
pip install -r requirements_cuda.txt
```

### 3. Download Model Files
Before running the process, download the necessary model files from the official website and place them inside the main folder.

### 4. Create Required Folders
Inside the main folder, create a `workspace` directory and inside it, create the following subdirectories:

```sh
workspace/
  ├── data_src/
  ├── data_dst/
  ├── model/
  ├── result/
```

Place the source images inside `workspace/data_src/` and the destination images inside `workspace/data_dst/`.

---

## Process Workflow
The process consists of four main steps:

### Step 1: Extract Faces
Extract faces from the source images:
```sh
python main.py extract --input-dir workspace/data_src --output-dir workspace/data_src/aligned
```

Extract faces from the destination images:
```sh
python main.py extract --input-dir workspace/data_dst --output-dir workspace/data_dst/aligned
```

### Step 2: Train the SAEHD Model
Train the model for head replacement:
```sh
python main.py train --training-data-src-dir workspace/data_src/aligned --training-data-dst-dir workspace/data_dst/aligned --model-dir workspace/model --model SAEHD
```

### Step 3: Merge with Blending
Merge with blending to create a natural look:
```sh
python main.py merge --input-dir workspace/data_dst --output-dir workspace/result --output-mask-dir workspace/result/masks --model-dir workspace/model --model SAEHD
```

### Step 4: Convert the Output
Finalize the face swap conversion:
```sh
python main.py convert --input-dir workspace/data_dst --output-dir workspace/result --model-dir workspace/model --model SAEHD
```

---

## Notes
- Ensure the `workspace` folder and all necessary subdirectories (`data_src`, `data_dst`, `model`, and `result`) exist before running the commands.
- The required model files must be placed in the main folder before running the process.
- Make sure your system meets the GPU requirements for running SAEHD efficiently.

---

Enjoy face swapping with SAEHD!

