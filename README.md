# Lip reading using Google Mediapipe and Long Short-Term Memory

Used Google’s Mediapipe library for feature extraction and calculate the
Euclidean distances, which are fed to an LSTM to make it effective
against any shift variance between the frames and also to reduce the
number of features to be stored as compared to other CNN-based
feature extraction methods.

## Dataset
- The dataset used for this project was the [BBC-LRW](https://www.robots.ox.ac.uk/~vgg/data/lip_reading/lrw1.html) dataset.
- The dataset consists of 500 classes of words spoken by different speakers, where
the videos are segments from various BBC news broadcasts.
- Each video has 29 frames and is 1.16 seconds in length. Because of the large
- The dataset is provided with a train, validation, and test split.
- Since only four classes are being chosen for performing classification, we capture the frames of
the videos from each of these four class folder.

## Feature extraction
- The lip region is distinguished in each frame by the landmark points. The face is
represented by 468 landmark points, each represented by their x, y coordinates.
- Out of these, 40 points track the lip contour region. This approach for feature
extraction is implemented using [Google’s Mediapipe Facemesh](https://google.github.io/mediapipe/solutions/face_mesh).
- The methodology focuses on the structural shape of the face by extracting
orientation of the lip contour region by isolating the information vital to the
process of lip reading in each frame.
- Mediapipe execute extraction of Region of Interest (ROI) by outputting the 40
landmark points tracing the lips.

## Feature classification
- After extracting the features from each frame, they are classified in order to
feed it to the LSTM network for training.
- Each of these 40 keypoints is represented by their x, y coordinates.
- For each frame, we first calculate the center of mass such that it is the mean of
the entire 40 (x, y) coordinates extracted.
- Subsequently, the Euclidean distances between the center of mass and each
of the keypoints are calculated and stored. This makes it effective against any
shift variance between the frames, and also reduces the number of features to
be stored as compared to other CNN-based feature extraction methods, thus
making it less memory-intensive.

## Long Short-Term Memory
- An LSTM layer accepts these features, which are now in 3-dimensional
arrays, and captures the spatiotemporal information from them.
- Layers that correspond to the output classes are utilized for performing
classification.
