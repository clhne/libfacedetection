# libfacedetection

This is a binary library for face detection and face landmark detection in images. 
The 32-bit and 64-bit dll files are provided.
To achieve better performance, the 64-bit dll is recommended.

examples/libfacedetect-example.cpp and examples/libfacedetectcnn-example.cpp shows how to use the library.

![Examples](/images/cnnresult.png "Detection example")


CNN-based Face Detection on Windows
-------------

| Method             |Time          | FPS         |Time          | FPS         |
|--------------------|--------------|-------------|--------------|-------------|
|                    |  X64         |X64          |  X64         |X64          |
|                    |Single-thread |Single-thread|Multi-thread  |Multi-thread |
|cnn (CPU, 640x480)  | 71.44ms      |  14.0       | 16.91ms      | 59.1        |
|cnn (CPU, 320x240)  | 18.21ms      |  54.9       |  4.60ms      | 217.4       |

* Face detection only, and no landmark detection included.
* Minimal face size ~10x10
* Intel(R) Core(TM) i7-7700 CPU @ 3.6GHz.

CNN-based Face Detection on ARM Linux (Raspberry Pi 3 B+)
-------------

| Method             |Time          | FPS         |Time          | FPS         |
|--------------------|--------------|-------------|--------------|-------------|
|                    |Single-thread |Single-thread|Multi-thread  |Multi-thread |
|cnn (CPU, 640x480)  |  710.2ms     |   1.4       |  231.5ms     |   4.3       |
|cnn (CPU, 320x240)  |  159.6ms     |   6.3       |   56.9ms     |  17.6       |
|cnn (CPU, 160x120)  |   36.2ms     |  27.6       |   13.3ms     |  75.2       |
|cnn (CPU, 128x96)   |   24.0ms     |  41.6       |    8.61ms    | 116.1       |

* Face detection only, and no landmark detection included.
* Minimal face size ~10x10
* Raspberry Pi 3 B+, Broadcom BCM2837B0, Cortex-A53 (ARMv8) 64-bit SoC @ 1.4GHz


Comparison on Windows
-------------

| Method             | Time        | FPS         |Time         | FPS         |Time         | FPS        | Misc   |
|--------------------|-------------|-------------|-------------|-------------|-------------|------------|--------|
|                    | Win32       |  Win32      |   X64       |  X64        |  X64        |X64         |        |
|                    |Single-thread|Single-thread|Single-thread|Single-thread|Multi-thread |Multi-thread|        |
|OpenCV              |  --         | --          | --          | --          | 12.33ms     |     81.1   | Yaw angle: -60 to 60 degrees|
|frontal             |  2.92ms     | 342.5       | 2.41ms      | 414.9       | 0.652ms     | 1533.1     | Yaw angle: -60 to 60 degrees|
|frontal-surveillance|  3.83ms     | 261.1       | 3.37ms      | 269.7       | 0.944ms     | 1059.8     | Yaw angle: -70 to 70 degrees |
|multiview           |  7.12ms     | 140.4       | 5.81ms      | 172.1       | 1.597ms     |  626.4     | Yaw angle: -90 to 90 degrees |
|multiview_reinforce | 10.95ms     |  91.3       | 9.15ms      | 109.3       | 2.725ms     |  367.0     | Yaw angle: -90 to 90 degrees |

* Face detection only, and no landmark detection included.
* 640x480 image size (VGA), scale=1.2, minimal window size = 48.
* Intel(R) Core(TM) i7-4770 CPU @ 3.4GHz.
* OpenCV classifier file: haarcascade_frontalface_alt.xml


Comparison on ARM
-------------

| Method             | Time   | FPS  | Misc   |
|--------------------|--------|------|--------|
|frontal             |  12.5ms| 80.0 | Yaw angle: -60 to 60 degrees|
|frontal-surveillance|  15.7ms| 63.7 | Yaw angle: -70 to 70 degrees |
|multiview           |  27.8ms| 36.0 | Yaw angle: -90 to 90 degrees |
|multiview_reinforce |  38.4ms| 26.0 | Yaw angle: -90 to 90 degrees |

* Face detection only, and no landmark detection included.
* 640x480 image size (VGA), scale=1.2, minimal window size = 48
* NVIDIA TK1 "4-Plus-1" 2.32GHz ARM quad-core Cortex-A15 CPU
* Multi-core parallelization is disabled.
* C programming language, and no SIMD instruction is used.

The dll cannot run on ARM. The library should be recompiled from source code for ARM compatibility. If you need the source code, a commercial license is needed.

Binary library for ARM
-------------
The binary evaluation library for ARM can be downloaded at https://github.com/OAID/YSQfastfd . The detection functions can only be called about 2000 times for evaluation.

Accuracy evaluation
-------------
FDDB: http://vis-www.cs.umass.edu/fddb/index.html

![Evaluation on FDDB](https://github.com/ShiqiYu/libfacedetection/blob/master/FDDB-results-of-4functions.png "Evaluation on FDDB")

* scale=1.08
* minimal window size = 16
* the heights of the face rectangles are scaled to 1.2 to fit the ground truth data in FDDB.


Author
-------------
* Shiqi Yu, <shiqi.yu@gmail.com>

Contributors
-------------
* Jia Wu
* Shengyin Wu
* Dong Xu

-------------
* The result image was taken by [Chloé Calmon](https://www.instagram.com/chloecalmon/).