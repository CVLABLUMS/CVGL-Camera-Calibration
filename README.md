# CAMERA CALIBRATION THROUGH GEOMETRIC CONSTRAINTS FROM ROTATION AND PROJECTION MATRICES

This code repository implements the camera calibration approach presented in the paper "Camera Calibration through Geometric Constraints from Rotation and Projection Matrices" available at [https://arxiv.org/abs/2402.08437](https://arxiv.org/abs/2402.08437). It offers efficient and accurate calibration using geometric constraints derived from rotation and projection matrices, providing an alternative to traditional methods.

This repository is valuable for:

- Researchers and developers interested in camera calibration using novel geometric constraints
- Anyone seeking to improve camera performance in robotics, autonomous vehicles or other vision applications

Key features include:

- Implementation of the proposed geometric constraint-based calibration algorithm
- Usage of the CARLA Simulator to generate an updated CVGL Camera Calibration dataset
- Clear and well-structured code for easy use and modification

# Weights for training and testing

All weights are available here:  https://drive.google.com/drive/folders/1wYDCMrJVgWAy3lJEGQsakYLUjYDl7i9s?usp=sharing

# Datasets

Updated CVGL Camera Calibration Dataset :
https://drive.google.com/drive/folders/1Zd4FPVq4xNU_MKz-gTxKtjj2axgH3IQ6?usp=drive_link

Daimler Pedestrian (Real Dataset): Click [here](https://www.gavrila.net/Datasets/Daimler_Pedestrian_Benchmark_D/Daimler_Stereo_Ped__Detection_/daimler_stereo_ped__detection_.html) for the Daimler Pedestrian Dataset.

Daimler Pedestrian format used for experiments:
https://drive.google.com/drive/folders/1Pe1nHpUe6PPtMpQpum-oKuD4v_aYXdfc?usp=drive_link

# About CVGL Camera Calibration Dataset

The dataset has been collected using the CARLA Simulator: https://carla.org//

This dataset comprises over 63,600 stereo RGB images, each with a resolution of 150x150 pixels. Where 10,400 images are from Town 3, 29,000 images are from Town 5 and 24,200 are from Town 6. We have generated more than 900 configurations to approximate real world conditions.

Focal Length is computed as follows: img_size[0]/(2 * np.tan(fov * np.pi/360))

Px and Py are computed as: img_size[0]/2

Fx = WINDOW_WIDTH/(2 * tan(fov * pi/360))

Fy = WINDOW_HEIGHT/(2 * tan(fov * pi/360))

Baseline is computed as: sqrt(x^2 + y^2 + z^2)

Disparity value is computed using the following:

stereo = cv2.StereoBM_create(numDisparities=16, blockSize=15)

disparity_map = stereo.compute(l_im, r_im)

disparity_value = np.mean(disparity_map)

xcam, ycam, zcam are computed as follows:

xcam = (Fx * x) / disparity_value
 
ycam = - (xcam / Fx) * (5 - Px)
                
zcam = (xcam / Fy) * (Py - 5)

xworld, yworld, zworld are computed as follows:

yworld = ycam + y

xworld = xcam * cos(pitch) + zcam * sin(pitch) + x

zworld = - xcam * sin(pitch) + zcam * cos(pitch) + z

Left Camera was  constant with the following configuration:

X = 0.2

Y = 0

Z = 0.2

Pitch = -1

Right Camera Configurations:

FOV with range from 50 to 110

X with range from 0.2 to 1

Y with range from 0.2 to 0.7

Z with range from 0.2 to 0.7

Pitch with range from -30 to 30

While making the dataset, we used the values as the difference between left and right camera. e.g. the value for X for first episode is 0.


# Citation

```
@misc{waleed2024camera,
      title={Camera Calibration through Geometric Constraints from Rotation and Projection Matrices}, 
      author={Muhammad Waleed and Abdul Rauf and Murtaza Taj},
      year={2024},
      eprint={2402.08437},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```

