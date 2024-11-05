# Lumincance-detection

## Project Overview
This project focuses on two primary tasks: **Image Classification** and **Image Correction**. Using a dataset of 138 images with various exposure levels, we trained classifiers to categorize images into one of three exposure categories (correctly exposed, underexposed, and overexposed). We also experimented with three methods for correcting improperly exposed images by applying **gamma correction** and evaluated the results using classification models and an entropy-based metric.

## Dataset
The dataset consists of **138 images** captured in diverse environments (indoor and outdoor) using an iPhone 12. The subjects include people, objects, and animals under different lighting conditions (natural, artificial, day, night, rainy). The dataset is balanced with:
- 46 **correctly exposed** images
- 46 **underexposed** images
- 46 **overexposed** images

### Pre-processing
- Images were converted to **double precision** and transformed into the **YCbCr color space**.
- Gamma correction was applied to the **Y (luminance)** channel to adjust brightness while preserving color information.

## Image Classification
For classification, we extracted 69 features from each image, including:
- **Mean**, **Variance**, and **Skewness** from RGB, HSV, and YCbCr color spaces.
- **Pixel Intensity Histograms** (15 features).
- **Edge Direction Histograms** (24 features).
- **Entropy** for each RGB channel.

Several classifiers were trained (SVM, KNN, Decision Trees, Ensemble Methods, Neural Networks), and **Efficient Linear SVM** achieved the best performance with an accuracy of **86%** on the test set.

### Feature Selection
To improve classification performance, we used the **Feature Importance** method to reduce the number of features to 10. This simplification boosted the model accuracy to **90%**.

## Image Correction
Three gamma correction methods were applied to underexposed and overexposed images:
1. **Preset Gamma Values**: Using preset values of **0.7** for underexposure and **1.3** for overexposure.
2. **Brute-Force Approach**: Testing a range of gamma values to minimize the Root Mean Square Error (RMSE).
3. **Optimization with fmincon**: Using the `fmincon` function to find the optimal gamma value by minimizing RMSE.

### Evaluation
- The gamma-corrected images were evaluated using the **Efficient Linear SVM** classifier, achieving an accuracy of **83%** on the full dataset.
- A new **Entropy-based metric** was developed to assess the correction quality, comparing the entropy of corrected images with that of correctly exposed images.

## Results and Discussion
- The **Efficient Linear SVM** classifier performed well after feature selection, achieving **86%** accuracy on test data.
- Gamma correction using **fmincon optimization** yielded the best results, with corrected images aligning closely with the luminance of correctly exposed images.
- The entropy-based metric provided a complementary assessment of image quality, though it did not outperform the classifier.

## Conclusions
The project demonstrated that reducing model complexity improves classification accuracy. Gamma correction was effectively applied to the images, and our approach of combining classification and entropy metrics provided robust results. Future improvements could include increasing dataset size and exploring more advanced evaluation metrics for gamma correction.

## Technology Stack
- Python
- MATLAB 


## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
