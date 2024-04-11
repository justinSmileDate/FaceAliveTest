一、对视频进行提取并训练
//提取假的视频帧(默认一个视频提取16张照片)
python gather_examples.py --input fake --output dataset/fake --detector face_detector

//提取真的视频帧
python gather_examples.py --input real --output dataset/real --detector face_detector

//训练
python train.py --dataset dataset --model liveness.model --le le.pickle

二、在开启本机摄像头上标记真假
//开摄像头
python liveness_demo.py --model liveness.model --le le.pickle --detector face_detector

//若测试一段现有视频则执行以下代码：
python testVideo.py --input test --model liveness.model --le le.pickle --detector face_detector   ）


---------------------------------------------------------------------------------
（gather_imges.py是针对输入的内容为图片的训练）

//提取假的帧（每张照片提取一次）
python gather_imges.py --input fake_imges --output dataset/fake_imges --detector face_detector

//提取真的帧
python gather_imges.py --input real_imges --output dataset/real_imges --detector face_detector

//训练
python train.py --dataset dataset --model liveness.model --le le.pickle

(train 跑不通的话  将57 行 labels = to_categorical(labels, 2)  2 换成 4  或者 4 换成2)