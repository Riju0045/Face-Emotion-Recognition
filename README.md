# Facial Expression Recognition

##  Project Overview

This project focuses on recognizing human facial expressions using Deep Learning and Computer Vision. A transfer learning approach based on **ResNet50**, a pretrained Convolutional Neural Network (CNN), is used to classify facial images into eight emotion categories.

The model takes a facial image as input and predicts the corresponding emotion using a softmax-based multiclass classification layer.

The project was implemented using Python and TensorFlow/Keras in Google Colab.

##  Objectives

- Develop a deep learning model for facial emotion recognition.
- Apply transfer learning using a pretrained ResNet50 architecture.
- Perform image preprocessing and data augmentation.
- Fine-tune the pretrained network for emotion classification.
- Evaluate model performance using classification metrics.
- Identify areas for improving classification accuracy and generalization.

##  Emotion Categories

The model classifies facial images into eight categories:

1. Anger
2. Contempt
3. Disgust
4. Fear
5. Happy
6. Neutral
7. Sad
8. Surprise

##  Dataset Description

The dataset contains facial images organized into separate training and testing directories, with subdirectories corresponding to the emotion labels.

| Parameter | Description |
|---|---|
| Total images | 30,626 |
| Training images | 16,108 |
| Test images | 14,518 |
| Number of classes | 8 |
| Image size | 224 × 224 pixels |
| Color channels | 3 (RGB) |
| Batch size | 32 |

The dataset is loaded using TensorFlow's `image_dataset_from_directory()` function.

##  Technologies Used

- **Programming Language:** Python
- **Deep Learning:** TensorFlow, Keras
- **Model Architecture:** ResNet50
- **Data Processing:** NumPy
- **Model Evaluation:** Scikit-learn
- **Visualization:** Matplotlib
- **Development Environment:** Google Colab

##  Model Architecture

The project uses ResNet50 pretrained on ImageNet as the feature extraction backbone.

The original classification head is replaced with a custom architecture designed for eight-class classification.

The model architecture consists of:

1. ResNet50 feature extractor
2. Global Average Pooling 2D
3. Dropout layer (0.3)
4. Dense layer with 128 neurons and ReLU activation
5. Dropout layer (0.2)
6. Dense output layer with 8 neurons and softmax activation

### Transfer Learning Strategy

**Stage 1 — Feature Extraction**

The pretrained ResNet50 layers are frozen while the newly added classification layers are trained.

**Stage 2 — Fine-Tuning**

The final 20 layers of ResNet50 are unfrozen for fine-tuning, while the earlier layers remain frozen. Batch normalization layers are kept frozen to help maintain training stability.

The Adam optimizer and sparse categorical cross-entropy loss are used for model training.

##  Data Preprocessing and Augmentation

The following preprocessing and augmentation techniques are implemented:

- Resize images to 224 × 224 pixels.
- Apply ResNet50-specific `preprocess_input()` preprocessing.
- Random horizontal flipping.
- Random rotation with a factor of 0.1.
- Random zooming with a factor of 0.1.
- Batch images using a batch size of 32.

Data augmentation introduces additional variation into training images and may help reduce overfitting.

##  Model Performance

The initial model evaluation produced the following results:

| Metric | Score |
|---|---:|
| Accuracy | 58% |
| Macro F1-score | 0.52 |
| Weighted F1-score | 0.56 |

### Class-wise Performance

- **Happy:** F1-score of 0.86
- **Neutral:** F1-score of 0.78
- **Contempt:** F1-score of 0.56
- **Sad:** F1-score of 0.47
- **Surprise:** F1-score of 0.43
- **Anger:** F1-score of 0.40
- **Fear:** F1-score of 0.39
- **Disgust:** F1-score of 0.23

The model performs relatively well for happy and neutral expressions but struggles with disgust, fear, and anger.

The reported metrics indicate that further improvements are needed to achieve more consistent classification across all emotion categories.

**Evaluation note:** The notebook uses the test directory as validation data during training. Therefore, these results should be treated as preliminary rather than as an independent final test estimate.

##  Evaluation Metrics

The model is evaluated using:

- **Accuracy:** Overall proportion of correct predictions.
- **Precision:** Reliability of predictions for each emotion class.
- **Recall:** Proportion of actual examples correctly identified.
- **F1-score:** Harmonic mean of precision and recall.
- **Confusion Matrix:** Visualization of correct classifications and misclassifications.

These metrics help identify classes that require further improvement.

##  Limitations

- Overall classification accuracy is moderate.
- Performance varies substantially across emotion categories.
- Disgust and fear have particularly low recall.
- Generalization to real-world webcam images has not been established.
- The original dataset's demographic composition and potential biases are not documented.
- The current evaluation procedure uses the test dataset during model selection.

The model predicts visible facial-expression categories and should not be interpreted as a definitive measurement of a person's internal emotional state.

##  Future Improvements

- Use a separate validation set and reserve the test set for final evaluation.
- Improve performance on underperforming emotion categories.
- Experiment with learning rates, dropout rates, batch sizes, and fine-tuning strategies.
- Compare ResNet50 with architectures such as EfficientNet and MobileNet.
- Add more comprehensive EDA and error analysis.
- Evaluate the model on unseen images and webcam inputs.
- Deploy the trained model through a Streamlit application.

## 📜 Disclaimer

This project is intended for educational and research purposes. Predictions may be inaccurate and should not be used as the sole basis for psychological, medical, employment, or other consequential decisions.
