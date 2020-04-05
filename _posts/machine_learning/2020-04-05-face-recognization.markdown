---
layout: post
title:  "Face recognization"
date:   2020-04-05 21:03:36 +0530
tags: "ai ml machine learning cnn face recognization"
---

Tổng hợp các open source code nổi tiếng về Face Recognition tại AICode: https://www.facebook.com/groups/3235479620010379/

1)Đầu tiên không thể thiếu là facenet của bác davidsandberg.
https://github.com/davidsandberg/facenet
Model bao gồm pretrain trên bộ dữ liệu CASIA-WebFace 450k ảnh/10k người và bộ dữ liệu VGGFace 3.3 triệu ảnh/9k người.

2) package face_recognition:
https://github.com/ageitgey/face_recognition
Đã được build thành package python, dễ cài đặt. Support face localization, detection, verification, embedding. Tài liệu hướng dẫn đầy đủ, chi tiết.

3) Thư viện dlib để phát hiện khuôn mặt.
https://github.com/davisking/dlib-models

4) Series các model face detection:
https://github.com/open-face/mtcnn

5) Series các model liên quan đến facenet:
https://github.com/topics/facenet

6) Một số pretrain model cũng khá nổi tiếng:
https://github.com/nyoki-mtl/keras-facenet
https://github.com/Abello966/keras-facenet
https://github.com/rcmalli/keras-vggface
https://github.com/faustomorales/keras-facenet
https://github.com/shanren7/real_time_face_recognition

7) Các model insight face:
https://github.com/deepinsight/insightface
https://github.com/foamliu/InsightFace-v2
https://github.com/TreB1eN/InsightFace_Pytorch
https://github.com/auroua/InsightFace_TF
https://github.com/kiselev1189/insightface-just-works
https://github.com/Fei-Wang/insightface
https://github.com/luckycallor/InsightFace-tensorflow
https://github.com/foamliu/InsightFace-PyTorch

8) Các model resnet face:
https://github.com/KaihuaTang/ResNet50-Pytorch-Face-Recognition
https://github.com/AruniRC/resnet-face-pytorch
https://github.com/habrman/FaceRecognition
https://github.com/LZQthePlane/Face-detection-base-on-ResnetSSD

9) Series pretrain model face recognition của bác baidu:
https://github.com/deepinsight/insightface/wiki/Model-Zoo

10) Series các pretrain model của cuộc thi aivivn được các bạn khai báo:
https://forum.machinelearningcoban.com/t/khai-bao-pretrained-models-cho-nhan-dien-nguoi-noi-tieng/4566/25

11) Khai báo của 1st cuộc thi aivivn nhận diện nhân vật nổi tiếng:
https://bitbucket.org/dungnb1333/dnb-facerecognition-aivivn/src/master/

12) Điều chỉnh color cho faces:
https://github.com/richzhang/colorization

13) Bộ dữ liệu về face:
VGGFace:https://www.robots.ox.ac.uk/~vgg/software/vgg_face/
CASIA-WEBFACE: https://pgram.com/dataset/casia-webface/
MS-1M-face dataset: https://megapixels.cc/msceleb/
LWD: http://vis-www.cs.umass.edu/lfw/
facescrub: http://vintage.winklerbros.net/facescrub.html