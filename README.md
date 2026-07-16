# Benchmarking Computer Vision Models on Edge Computing Devices

**Final Year Project — BS Computer Engineering, Information Technology University (ITU), Lahore**
Supervised by Dr. Rehan Hafiz & Dr. Rehan Ahmed | Nov 2025 – Jun 2026

A systematic benchmarking study evaluating six lightweight computer vision models across two affordable single-board computers — **Raspberry Pi 4 Model B** and **Orange Pi 3 LTS** — under real-world, CPU-only conditions across four practical application domains.

## Team
- Maryam Aftab (BSCE22031)
- Hoor-ul-Ain Amir (BSCE22037)
- Rameeza Rahim (BSCE22052)

## 🎯 Project Overview
Most computer vision models are built and benchmarked for high-performance GPUs — but real deployments in budget-constrained settings (like Pakistan) run on cheap, CPU-only edge hardware. This project builds a standardized benchmarking framework to answer a practical question: **which model–device combination actually works best for real-time deployment on a tight budget?**

We benchmarked models across four real-world tasks:
- General **Object Detection**
- **License Plate Recognition** (custom Pakistani number plate dataset)
- **Intrusion Detection** (zone-based alarm system)
- **Age & Gender Classification** (custom local demographic dataset)

A key contribution is the creation of **original, Pakistan-specific datasets** for number plates and age/gender classification — existing public datasets are almost entirely Western/East Asian and don't represent local plate formats, fonts, or demographics.

## 🖥️ Hardware Benchmarked
| Device | CPU | RAM | Price (approx.) |
|---|---|---|---|
| Raspberry Pi 4 Model B | Quad-core ARM Cortex-A72 | 4 GB | Rs. 25,000 |
| Orange Pi 3 LTS | Quad-core ARM Cortex-A53 (Allwinner H6) | 2 GB | Rs. 18,000 |

Both devices ran entirely in **CPU-only mode** — no GPU or NPU acceleration — to simulate realistic low-budget deployment conditions.

## 🧠 Models Evaluated
| Model | Task | Format | Training |
|---|---|---|---|
| YOLOv8n | Object Det., Plate, Intrusion, Age/Gender | ONNX | Fine-tuned |
| YOLOv5n | License Plate Detection | ONNX | Fine-tuned |
| YOLOv5s | Intrusion Detection | ONNX | Fine-tuned |
| MobileNet SSD v2 | Base Object Detection | TFLite | Pre-trained |
| Caffe Classifier | Age and Gender | Caffe | Fine-tuned |
| WideResNet + OpenCV | Age and Gender | ONNX | Fine-tuned |

## 🛠️ Tech Stack
`Python` `OpenCV` `PyTorch` `TensorFlow` `ONNX` `TFLite` `Edge Impulse` (annotation) `Balena Etcher`

## ⚙️ Methodology
1. **Data Collection** — Captured original images/video via 1080P USB webcam across all 4 task domains, including custom Pakistani number plate and demographic datasets.
2. **Annotation** — Labeled using Edge Impulse, exported in YOLO format.
3. **Fine-Tuning** — Pre-trained weights fine-tuned on the custom datasets per task.
4. **Export** — YOLO models exported to ONNX; MobileNet SSD exported to TFLite.
5. **Deployment** — OS flashed to SD cards via Balena Etcher, models deployed on both devices in CPU-only mode.
6. **Benchmarking** — Measured inference time (ms), FPS, mAP50/mAP50-95, RAM usage, CPU usage, and task-specific accuracy/F1 score for every model–device pair.

## 📊 Key Results

**Age & Gender Classification** (custom 205-image dataset)
| Model | Device | FPS | Inference (ms) | RAM (MB) | Gender Acc. |
|---|---|---|---|---|---|
| WideResNet + OpenCV | RPi 4 | 1.74 | 554.6 | 3171 | **99.00%** |
| YOLOv8n + Caffe | RPi 4 | **2.18** | **436.5** | **93** | 74.00% |

**License Plate Recognition**
| Model | Device | FPS | Inference (ms) | RAM (MB) | F1 Score |
|---|---|---|---|---|---|
| YOLOv8n | RPi 4 | **1.20** | **804.9** | **73** | **92.92%** |
| YOLOv5n | RPi 4 | 0.40 | 2279.5 | 281 | 76.86% |

**Object Detection**
| Model | Device | FPS | Inference (ms) | RAM (MB) |
|---|---|---|---|---|
| MobileNet SSD | RPi 4 | **5.26** | **114.9** | **14** |
| YOLOv8n | RPi 4 | 0.80 | 1196.3 | 55 |

**Intrusion Detection** (zone-based alarm)
| Model | Device | FPS | Inference (ms) | RAM (MB) | F1 Score |
|---|---|---|---|---|---|
| YOLOv8n | RPi 4 | **1.43** | **476.1** | 499 | 79.50% |
| YOLOv8n | Orange Pi 3 | 0.78 | 971.6 | 564 | **83.00%** |

## 🏆 Key Findings
- **Raspberry Pi 4 was the stronger overall device**, delivering the best single-model performance in every task category despite Orange Pi 3 being the cheaper option.
- **MobileNet SSD on RPi 4** was the standout result of the entire study — 5.26 FPS, 114.9ms inference, and just 14 MB RAM, making genuinely real-time edge deployment possible with zero hardware acceleration.
- **YOLOv8n proved the most versatile model**, performing competitively across speed, accuracy, and memory efficiency for license plate detection and intrusion detection — the best single-model recommendation for multi-task edge deployment.
- Accuracy and raw processing speed don't always move together: YOLOv8n scored a *higher* F1 (83.00%) on the weaker Orange Pi 3 than on RPi 4 (79.50%) for intrusion detection.
- The Rs. 7,000 price premium of the Raspberry Pi 4 over the Orange Pi 3 LTS is justified by consistently faster inference and better memory efficiency — but the Orange Pi 3 remains a legitimate budget option where memory efficiency matters more than raw speed (e.g. WideResNet age estimation used 2,278 MB *less* RAM on Orange Pi 3).

## 🇵🇰 Local Impact
Beyond the hardware benchmarks, this project produced **original Pakistan-specific datasets** for number plate detection and age/gender classification — covering regional plate formats and demographic variation across Punjab, Balochistan, Khyber Pakhtunkhwa, and Karachi — filling a real gap left by existing Western/East-Asian-centric public datasets.

## 📌 My Contribution (Maryam Aftab)
- Literature review and research gap analysis
- Data annotation and labeling (Edge Impulse, YOLO format)
- Performance benchmarking across all model–device combinations (FPS, latency, memory, accuracy)
- Final review, proofreading, and submission

## 📄 Full Report
The complete final year project report — including full methodology, literature review, cost breakdown, and detailed per-task analysis — is included in this repository.

## 👩‍💻 Authors
Maryam Aftab · Hoor-ul-Ain Amir · Rameeza Rahim — Department of Computer Engineering, ITU Lahore
