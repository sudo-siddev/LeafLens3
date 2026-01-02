# CultiKure - Plant Disease Prediction Web Application

CultiKure is a web-based tool designed to help users detect and address diseases in plants. By analyzing images of plant leaves, this application employs advanced AI technology to identify potential plant health issues, ensuring healthier crops and better yields.

## Key Features:

- **AI-Powered Disease Detection:** Upload plant leaf images to get real-time analysis and detection of diseases.
- **Informative Reports:** Receive detailed reports about detected diseases, including descriptions, preventive measures, and product recommendations.
- **Supplement Market:** Explore a selection of supplements and fertilizers to support plant health.
- **User-Friendly Interface:** An intuitive and easy-to-navigate interface for a seamless user experience.

## Technologies Used:

- **AI Model:** ResNet50 (Residual Neural Network) with Transfer Learning for image classification.
- **Deep Learning Framework:** PyTorch
- **Web Framework:** Flask for the back-end.
- **Front-end:** HTML, CSS, JavaScript.
- **Libraries/Frameworks:** Bootstrap for styling.

## How to Use:

1. Navigate to the CultiKure Web Application
2. Upload an image of a plant leaf.
3. Receive detailed information about the detected disease, including tips and product recommendations.

## Why Plant Disease Detection Matters:

Plant diseases can significantly impact crop health and yield. Early detection and intervention are crucial. CultiKure helps users identify and address potential issues, ensuring healthier crops and better yields.

## Quick Start:

### Prerequisites
- Python 3.7 or higher
- Git

### Installation & Running the Project

1. **Clone the repository:**
   ```shell
   git clone https://github.com/yourusername/CultiKure.git
   cd plant-disease
   ```

2. **Navigate to the App directory:**
   ```shell
   cd App
   ```

3. **Create a virtual environment:**
   ```shell
   python -m venv venv
   ```
   *Or use `.venv` as the name:*
   ```shell
   python -m venv .venv
   ```

4. **Activate the virtual environment:**
   
   **For Windows:**
   ```shell
   venv\Scripts\activate
   ```
   *Or if you named it `.venv`:*
   ```shell
   .venv\Scripts\activate
   ```
   
   **For Linux/Mac:**
   ```shell
   source venv/bin/activate
   ```
   *Or if you named it `.venv`:*
   ```shell
   source .venv/bin/activate
   ```

5. **Install dependencies:**
   ```shell
   pip install -r requirements.txt
   ```

6. **Run the Flask application:**
   ```shell
   python app.py
   ```

7. **Open your browser and navigate to:**
   ```
   http://127.0.0.1:5000
   ```

That's it! The application should now be running locally.

## Model Training

This project uses a **ResNet50** deep learning model trained on the **PlantVillage dataset** for plant disease classification.

### Dataset
- **Dataset Name:** PlantVillage Dataset
- **Classes:** 39 plant disease classes
- **Source:** PlantVillage dataset (available on Kaggle)
- **Location:** `dataset/raw/` (must be extracted before training)

### Model Architecture
- **Base Model:** ResNet50 (pretrained on ImageNet)
- **Transfer Learning:** Full fine-tuning using ImageNet pretrained weights (IMAGENET1K_V2)
- **Custom Classifier:** Final fully connected layer replaced for 39 disease classes
- **Input Size:** 224×224 RGB images

### Training Parameters
- **Optimizer:** Adam
- **Learning Rate:** 0.001
- **Batch Size:** 32
- **Epochs:** 20
- **Learning Rate Scheduler:** StepLR (reduces LR by 0.1× every 7 epochs)
- **Loss Function:** CrossEntropyLoss
- **Data Augmentation:** Random horizontal flip, rotation (±10°), color jitter

### Dataset Split
- **Training:** 70%
- **Validation:** 15%
- **Test:** 15%

### Evaluation Metrics
The model is evaluated using:
- **Accuracy:** Overall classification accuracy
- **Precision, Recall, F1-Score:** Macro and weighted averages
- **Per-Class Metrics:** Precision, recall, F1-score for each disease class
- **Confusion Matrix:** Visual representation of classification performance

### Training the Model

1. **Ensure the dataset is in place:**
   ```shell
   # The PlantVillage dataset should be extracted to:
   dataset/raw/
     ├── Apple___Apple_scab/
     ├── Apple___Black_rot/
     ├── ... (all 39 classes)
   ```

2. **Navigate to the App directory:**
   ```shell
   cd App
   ```

3. **Run the training script:**
   ```shell
   python train_model.py
   ```
   
   The script will:
   - Automatically create train/val/test splits from `dataset/raw/` if they don't exist
   - Train the ResNet50 model with transfer learning
   - Save the trained model to `trained_model.pth`
   - Generate evaluation metrics and plots in `training_results/`

4. **Training Output:**
   - `trained_model.pth`: Trained model weights
   - `training_results/training_history.png`: Training/validation loss and accuracy curves
   - `training_results/confusion_matrix_validation.png`: Validation set confusion matrix
   - `training_results/confusion_matrix_test.png`: Test set confusion matrix
   - `training_results/validation_metrics.txt` & `.json`: Validation metrics
   - `training_results/test_metrics.txt` & `.json`: Test set metrics (final evaluation)
   - `training_results/training_summary.json`: Complete training summary

### Expected Performance
With proper training, the model typically achieves:
- **Test Accuracy:** 85-95% (depending on dataset quality and training)
- **F1-Score:** 0.85-0.95 (macro average)

## Video-Demonstration
[Video.mp4](https://youtu.be/cbCVkRAjhgE)




