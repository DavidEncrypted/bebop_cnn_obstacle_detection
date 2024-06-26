# Bebob cnn obstacle detection
This repo contains the code to create a custom version of MobileNetv3, called MobileNetv3-tiny. This was designed specifically to be used onboard of a parrot bebop drone. The model is small enough to run with 6 FPS. The repo also contains the code/instructions to port the generated model to c to be able to compile it for arm hardware.


# Dataset
For the competition we collected 7000 images, these are used to train a cnn to detect obstacles.

Download the dataset from:
```
https://mega.nz/file/YbsFxZrK#wl90ytVbSUDmdfBoJq5j4N9VfpQjw3vUHddsxzjS5AE
```
Extract the content into `./data/`
You should end up with a folder `./data/collected_data/` and `./data/existing_data/`

# Installation
Install onnx2c, used to convert the model onnx to c
`git clone https://github.com/kraiskil/onnx2c.git`

Install:
```
pip install -r requirements.txt
```
# Run
1. Run through all the cells in `dataset_create.ipynb`.
2. Run all the cells in `custom_cnn.ipynb`.
3. Follow onnx2c instructions to convert output onnx file to c
4. Move the c file to the paparazzi repo/branch
## ...
MobileNetv3 from:

https://github.com/d-li14/mobilenetv3.pytorch/tree/master





TODOS:

Add onnx2c repo


## Optimization notes

```
cnn profiling
block 0 takes almost all of the execution time

Setting up 'bottom_camera'... ok
Block 0: Execution time: 0.050126 seconds
Block 1: Execution time: 0.000568 seconds
Block 2: Execution time: 0.008070 seconds
Block 4: Execution time: 0.004868 seconds
Block 4: Execution time: 0.005792 seconds
Block 5: Execution time: 0.006409 seconds
Block convfinal: Execution time: 0.002716 seconds
Block classifier: Execution time: 0.000206 seconds


Block 0: Execution time: 0.075067 seconds
Block 1: Execution time: 0.000871 seconds
Block 2: Execution time: 0.008222 seconds
Block 4: Execution time: 0.006753 seconds
Block 4: Execution time: 0.006158 seconds
Block 5: Execution time: 0.007875 seconds
Block convfinal: Execution time: 0.002295 seconds
Block classifier: Execution time: 0.000245 secondsz


-O3

Block 0: Execution time: 0.041479 seconds
Block 1: Execution time: 0.000575 seconds
Block 2: Execution time: 0.004347 seconds
Block 4: Execution time: 0.004145 seconds
Block 4: Execution time: 0.003369 seconds
Block 5: Execution time: 0.005252 seconds
Block convfinal: Execution time: 0.002370 seconds
Block classifier: Execution time: 0.000153 secondsa


85.30973451327434 Test acc for Tinyv4



84.8672 test acc for Tinyv5

Tinyv5 --------------
Block 0: Execution time: 0.008707 seconds
Block 0, conv0: Execution time: 0.008532 seconds
Block tot classifier: Execution time: 0.011883 seconds
Block classifier: Execution time: 0.000330 seconds
Obstacle straight ahead! | Nowhere to go!, turn around!
Elapsed time: 13368 microseconds
Elapsed time, image moving: 615 microseconds
Block 0: Execution time: 0.025925 seconds
Block 0, conv0: Execution time: 0.025491 seconds
Block tot classifier: Execution time: 0.017567 seconds
Block classifier: Execution time: 0.000434 seconds
Obstacle straight ahead! | Nowhere to go!, turn around!
Elapsed time: 12471 microseconds
Elapsed time, image moving: 786 microseconds
Block 0: Execution time: 0.016623 seconds
Block 0, conv0: Execution time: 0.016368 seconds
Block tot classifier: Execution time: 0.014190 seconds
Block classifier: Execution time: 0.000498 seconds
Obstacle straight ahead! | Nowhere to go!, turn around!
Elapsed time: 16289 microseconds
Elapsed time, image moving: 453 microseconds
Block 0: Execution time: 0.013718 seconds
Block 0, conv0: Execution time: 0.013460 seconds
Block tot classifier: Execution time: 0.014293 seconds
Block classifier: Execution time: 0.000399 seconds
Obstacle straight ahead! | Nowhere to go!, turn around!
Elapsed time: 15723 microseconds
Elapsed time, image moving: 1006 microseconds
Block 0: Execution time: 0.011573 seconds
Block 0, conv0: Execution time: 0.011459 seconds
Block tot classifier: Execution time: 0.015876 seconds
Block classifier: Execution time: 0.000222 seconds
Obstacle straight ahead! | Turn left!
Elapsed time: 18394 microseconds
Elapsed time, image moving: 508 microseconds
Block 0: Execution time: 0.009957 seconds
Block 0, conv0: Execution time: 0.009745 seconds
Block tot classifier: Execution time: 0.017316 seconds
Block classifier: Execution time: 0.000219 seconds
Obstacle straight ahead! | Nowhere to go!, turn around!
Elapsed time: 17529 microseconds
Elapsed time, image moving: 464 microseconds
Block 0: Execution time: 0.009248 seconds
Block 0, conv0: Execution time: 0.009189 seconds
Block tot classifier: Execution time: 0.011393 seconds
Block classifier: Execution time: 0.000321 seconds
Obstacle straight ahead! | Nowhere to go!, turn around!
Elapsed time: 12812 microseconds
Elapsed time, image moving: 398 microseconds
Block 0: Execution time: 0.021518 seconds
Block 0, conv0: Execution time: 0.021296 seconds
Block tot classifier: Execution time: 0.011078 seconds
Block classifier: Execution time: 0.000208 seconds
Obstacle straight ahead! | Nowhere to go!, turn around!
Elapsed time: 13261 microseconds
Elapsed time, image moving: 445 microseconds
Block 0: Execution time: 0.010216 seconds
Block 0, conv0: Execution time: 0.010107 seconds
Block tot classifier: Execution time: 0.009584 seconds
Block classifier: Execution time: 0.000510 seconds
Obstacle straight ahead! | Nowhere to go!, turn around!
Elapsed time: 12030 microseconds
Elapsed time, image moving: 836 microseconds
Block 0: Execution time: 0.033459 seconds
Block 0, conv0: Execution time: 0.033341 seconds
Block tot classifier: Execution time: 0.010470 seconds
Block classifier: Execution time: 0.000279 seconds
Obstacle straight ahead! | Nowhere to go!, turn around!
Elapsed time: 12881 microseconds
Elapsed time, image moving: 569 microseconds
Block 0: Execution time: 0.016183 seconds
Block 0, conv0: Execution time: 0.016006 seconds
Block tot classifier: Execution time: 0.013583 seconds
Block classifier: Execution time: 0.000233 seconds
Obstacle straight ahead! | Nowhere to go!, turn around!
Elapsed time: 16549 microseconds



v6 op drone:
230680 microseconds

v7 op drone:
183558 microseconds
```
