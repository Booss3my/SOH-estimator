# SOH-estimator
Real-time Li-Ion state of health estimation using LSTMS (Proof Of Concept)


This notebook presents my implementation of a real-time battery health estimation system developed during my internship at Serma Technologies.

In this system, the model utilizes battery signals, specifically the voltage first derivative recorded during the charging process, to predict battery cell capacity. It is referred to as real-time because the capacity variations between charges are minimal, typically less than 0.001% of the total capacity.

The model architecture consists of two LSTM cells followed by a final linear layer. The training process is as follows:
<p align="center">
<img src="https://github.com/Booss3my/Notebooks/assets/56868809/5674801c-7e41-44d0-8aa5-fdf483006fae" width="50%" height="50%" />
</p>
We define a fixed window size and sample windowed versions of the input signal.
These windowed signals are used to train the model.

<p align="center">
<img src="https://github.com/Booss3my/Notebooks/assets/56868809/cdcc88b4-a6b9-4a01-831e-3657681c0423" width="50%" height="50%" />
</p>

To evaluate the model's performance, two test cells are utilized.
Test cell 1             |  Test cell 2
:-------------------------:|:-------------------------:
![image](https://github.com/Booss3my/Notebooks/assets/56868809/e3ce65c1-02b2-448b-a0ea-11138c8b2c5f) |  ![image](https://github.com/Booss3my/Notebooks/assets/56868809/fcb79855-f0c6-4d18-bf4b-b80dcac74efc)

However, the model faces challenges when predicting the value 0. This difficulty arises from the near-zero slope (-∞) of the Sigmoid function, which significantly diminishes gradients and slows down parameter updates for this type of output.

During inference, the model's performance improves by averaging its predictions across multiple samples from the same signal.

 
