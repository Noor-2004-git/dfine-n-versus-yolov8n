# NEU Surface Defect Detection: D-FINE-N vs YOLOv8n

## Overview

This project evaluates and compares two state-of-the-art object detection models, **D-FINE-N** and **YOLOv8n**, on the **NEU Surface Defect Detection Dataset**. The goal is to identify and localize six common steel surface defects while analyzing model accuracy, inference speed, and deployment efficiency.

### Defect Classes

* Crazing
* Inclusion
* Patches
* Pitted Surface
* Rolled-in Scale
* Scratches

---

## Dataset

**NEU Surface Defect Database**  https://drive.google.com/drive/folders/1Brx2YlCJN6RIPSytcxGT3jgNgBpl0_yU?usp=sharing [Dataset, COCO FORMAT ALSO AVAILABLE]

* Total Classes: 6
* Annotation Format: COCO (for D-FINE) and YOLO format (for YOLOv8n)
* Input Resolution: 640 × 640

---

## Models Evaluated

### D-FINE-N

* Backbone: HGNetv2-B0
* Transformer Layers: 2
* Training Epochs: 100
* Best Checkpoint: `best_stg1.pth`   https://drive.google.com/file/d/1ULdGjRDSJ-KATEOocbxMQgJwyzZGqY_m/view?usp=sharing

### YOLOv8n

* Model: YOLOv8 Nano
* Fine-tuned from pretrained weights
* Maximum Epochs: 100
* Early Stopping: Patience = 20
* Best Checkpoint: `best.pt`

---

## Experimental Setup

| Parameter  | Value                      |
| ---------- | -------------------------- |
| GPU        | NVIDIA Tesla T4            |
| Image Size | 640 × 640                  |
| Batch Size | 4 (D-FINE), 16 (YOLOv8n)   |
| Framework  | PyTorch                    |
| Dataset    | NEU Surface Defect Dataset |

---

## Performance Comparison

| Metric     | D-FINE-N | YOLOv8n |
| ---------- | -------: | ------: |
| mAP@50:95  |   22.90% |  41.35% |
| mAP@50     |   41.20% |  77.33% |
| Latency    | 20.99 ms | 8.11 ms |
| FPS        |    47.63 |  123.20 |
| Model Size |   138 MB |  6.0 MB |
Latency tested on a set of 10 images same for both DFINE n and YOLOv8n

---

## Key Findings

### D-FINE-N

**Advantages**

* Transformer-based architecture
* Strong localization capability
* Improved performance after extended training

**Limitations**

* Larger model size
* Higher inference latency
* Lower mAP on the NEU dataset

### YOLOv8n

**Advantages**

* Highest detection accuracy
* Lowest latency
* Highest FPS
* Extremely lightweight deployment model

**Limitations**

* Slightly less sophisticated architecture compared to transformer-based detectors

---

## Notes on Training

D-FINE does not provide built-in early stopping support. Therefore, training was conducted for 100 epochs and the best validation checkpoint (`best_stg1.pth`) was selected for evaluation.

YOLOv8n was trained with a maximum of 100 epochs and early stopping (patience = 20). The best checkpoint (`best.pt`) was used for final evaluation.

---

## Conclusion

On the NEU Surface Defect Detection dataset, YOLOv8n achieved significantly better detection performance while maintaining substantially lower latency and model size. For real-time industrial deployment scenarios where speed and memory efficiency are critical, YOLOv8n proved to be the more suitable model.

---

## Repository Structure

```text
.
├── COCOn/
├── YOLO/
├── configs/
├── tools/
├── src/
├── output/
│   └── dfine_hgnetv2_n_neu/
│       └── best_stg1.pth
├── yolo_finetune/
│   └── yolov8n_neu-2/
│       └── best.pt
└── README.md
```

## Author

**Noor Tandon**

Computer  Engineering Student
Thapar Institute of Engineering and Technology
