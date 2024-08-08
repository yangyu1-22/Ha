# Glasses-noglasses
This project can help people costomize their own glasses style
![https://www.kaggle.com/datasets/adnanzaidi/glasses] (direct image link here)
#  The Algorithm
This model is created on jetson nano and trained on datasets of glasses/nonglasses
# Running this project
Training a Network

1.connect to your nano and open Visual Studio Code. Make sure you download the resource(the image)

2. cd to nvidia/jetson-inference/
 run this code [echo 1 | sudo tee /proc/sys/vm/overcommit_memory]

3. back in the jetson-inference folder, run [./docker/run.sh to run the docker container.] (You may have to re-enter your nvidia password at this step)

4.change directories so you are in 'jetson-inference/python/training/classification'

5.run this code to train [python3 train.py --model-dir=models/glasses-noglasses data/glasses-noglasses]

6. When running the model you can also specify the value of how many epochs and batch sizes you want to run.
  [ --batch-size=NumberOfBatchFiles] [--workers=NumberOfWorkers] [--epochs=NumberOfEpochs]

Exporting the Network

7.Make sure you are in the docker container and in jetson-inference/python/training/classification
  Run the onnx export script.
  [python3 onnx_export.py --model-dir=models/glasses-noglasses]

8.Look in the jetson-inference/python/training/classification/models/cat_dog folder to see if there is a new model called 'resnet18.onnx' there. That is your re-trained model!

Processing Images

9. Exit the docker container by pressing Ctl + D.

   On your nano, navigate to the jetson-inference/python/training/classification directory.

10. Set the NET and DATASET variables
NET=models/glasses-noglasses
DATASET=data/glasses-noglasses

11.
Run this command to see how it operates on an image from the cat folder.
[imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/row-7-column-4.jpg output.jpg]

video link [https://youtu.be/nPOMfKQz0wo ]


