# Face models

The model files are not committed to the repository. Download them from the OpenCV Model Zoo and place them in this folder:

- **YuNet** face detector: https://github.com/opencv/opencv_zoo/tree/main/models/face_detection_yunet
- **SFace** face recognizer: https://github.com/opencv/opencv_zoo/tree/main/models/face_recognition_sface

Both are `.onnx` files and load with `cv2.FaceDetectorYN` and `cv2.FaceRecognizerSF`.
