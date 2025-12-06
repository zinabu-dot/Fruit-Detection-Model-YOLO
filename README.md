fruit-detection/
│
├── config/
│   ├── data.yaml                # YOLO dataset config
│   ├── train.yaml               # training hyperparams
│   ├── model.yaml               # model architecture config
│   ├── inference.yaml           # thresholds, NMS, etc.
│   └── deployment.yaml          # server settings
│
├── data/
│   ├── raw/                     # original dataset (images)
│   ├── labels_raw/              # raw annotations
│   ├── processed/               # cleaned/resized/augmented data
│   ├── train/                   # YOLO-ready structure
│   ├── val/
│   └── test/
│
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_training_experiments.ipynb
│   └── 04_evaluation_visuals.ipynb
│
├── src/
│   ├── data/
│   │   ├── prepare_dataset.py    # resizing, splitting, augmenting
│   │   └── label_converter.py    # convert COCO/VOC → YOLO format
│   │
│   ├── training/
│   │   ├── train.py              # central training script
│   │   ├── callbacks.py          # custom logging, early stopping
│   │   └── augmentations.py      # custom Albumentations transforms
│   │
│   ├── inference/
│   │   ├── predict.py            # run detection on single images
│   │   ├── batch_infer.py        # infer on folders or videos
│   │   └── postprocess.py        # NMS, threshold adjustments
│   │
│   ├── serving/
│   │   ├── api.py                # FastAPI endpoint for detection
│   │   └── utils.py
│   │
│   └── utils/
│       ├── helpers.py
│       └── visualization.py      # draw boxes, metrics
│
├── models/
│   ├── yolov8n_fruit.pt
│   ├── yolov8s_fruit.pt
│   └── best.pt                   # best checkpoint from training
│
├── deployments/
│   ├── docker/
│   │   ├── Dockerfile.api
│   │   ├── Dockerfile.inference
│   │   └── docker-compose.yaml
│   └── edge/
│       └── jetson_deploy.md      # instructions for Jetson/Coral/Nano
│
├── tests/
│   ├── test_dataset.py
│   ├── test_training.py
│   └── test_inference.py
│
├── scripts/
│   ├── run_training.sh
│   ├── convert_labels.sh
│   └── evaluate.sh
│
├── results/
│   ├── confusion_matrix.png
│   ├── pr_curve.png
│   └── metrics.json
│
├── README.md
├── requirements.txt
└── pyproject.toml
