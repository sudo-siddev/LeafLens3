# Training Quick Start Guide

**Quick reference for running the training pipeline.**

---

## Prerequisites

1. ✅ Python 3.7+ installed
2. ✅ PlantVillage dataset downloaded and extracted to `dataset/raw/`
3. ✅ Virtual environment created and activated
4. ✅ Dependencies installed (`pip install -r requirements.txt`)

---

## Dataset Location

```
project_root/
└── dataset/
    └── raw/              ← Place PlantVillage dataset here
        ├── Apple___Apple_scab/
        ├── Apple___Black_rot/
        └── ... (all 39 classes)
```

**Download from:** https://www.kaggle.com/datasets/abdallahalidev/plantvillage-dataset

---

## Training Commands

```bash
# 1. Navigate to App directory
cd App

# 2. Activate virtual environment
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# 3. Run training
python train_model.py
```

That's it! The script will:
- ✅ Automatically create train/val/test splits
- ✅ Train the ResNet50 model
- ✅ Save model to `trained_model.pth`
- ✅ Generate all metrics and plots in `training_results/`

---

## Expected Output Files

After training completes:

```
App/
├── trained_model.pth                    ← Trained model weights
└── training_results/
    ├── training_history.png            ← Training curves
    ├── confusion_matrix_validation.png ← Validation confusion matrix
    ├── confusion_matrix_test.png       ← Test confusion matrix
    ├── validation_metrics.txt          ← Validation metrics (human-readable)
    ├── validation_metrics.json         ← Validation metrics (structured)
    ├── test_metrics.txt                ← Test metrics (human-readable) ⭐ FINAL
    ├── test_metrics.json               ← Test metrics (structured) ⭐ FINAL
    └── training_summary.json           ← Complete training summary
```

---

## Training Time Estimate

- **Dataset Preparation:** 5-15 minutes (one-time only)
- **Training:** 2-6 hours (depends on GPU/CPU)

---

## Troubleshooting

**Error: "Raw dataset not found"**
- ✅ Ensure PlantVillage dataset is extracted to `dataset/raw/`
- ✅ Check that `dataset/raw/` contains class folders (e.g., `Apple___Apple_scab/`)

**Error: "Module not found"**
- ✅ Install dependencies: `pip install -r requirements.txt`
- ✅ Ensure virtual environment is activated

**Out of memory during training**
- ✅ Reduce `BATCH_SIZE` in `train_model.py` (line 24)
- ✅ Use a machine with more RAM/GPU memory

---

## For More Details

- 📖 Full documentation: See `ACADEMIC_DOCUMENTATION.md`
- 📖 README: See `README.md` (Model Training section)
- 📖 Training code: See `App/train_model.py` (fully commented)

---

**Ready to train! Run `python train_model.py` from the App directory.**




