# Lip reading using Google Mediapipe and Long Short-Term Memory

Used Google’s Mediapipe library for feature extraction and calculate the
Euclidean distances, which are fed to an LSTM to make it effective
against any shift variance between the frames and also to reduce the
number of features to be stored as compared to other CNN-based
feature extraction methods.
