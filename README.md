
# Gundog.Compass

## Tilt Compensated Compass Method

### Description

Gundog.Compass is an R function designed to compute the body orientation angles (pitch, roll, and yaw — also known as heading) from supplied tri-axial accelerometer and magnetometer data. This script is typically used in tandem with Gundog.Tracks to compute body heading prior to dead-reckoning. The function features optional initial soft and hard iron distortion correction for magnetometer data, as well as tag rotation correction to ensure that angles are accurately computed. Users can choose between a standard Euler angle approach or the SAAM (Super-fast Attitude of Accelerometer and Magnetometer) method, which leverages quaternions for enhanced performance.

### Required Inputs

- **Tri-axial Magnetometer Data**: Magnetic field measurements along x, y, and z axes (`mag.x`, `mag.y`, `mag.z`).
- **Tri-axial Static Acceleration Data**: Gravity components of acceleration along x, y, and z axes (`acc.x`, `acc.y`, `acc.z`). These are not raw accelerometer data. Typically, they are derived using a running mean over a window of 1-2 seconds.
- **Marked Events Data (ME)**: Specifies the calibration period for magnetic correction, denoted by `M`. Calibration should involve slow rotations, covering all possible orientations (roll, pitch, and yaw) to detect hard and soft iron errors.
- **Method for Magnetic Correction**: Eight different methods can be applied for correction, ranging from simple orthogonal rescaling to complex rotated ellipsoid adjustments. Method 3 is recommended for good calibration periods, while Method 1 is suitable when calibration coverage is incomplete.

### Additional Inputs

- **Coordinate Frame Inputs**: Inputs such as `acc.ref.frame`, `positive.g`, and `mag.ref.frame` are used to convert the device’s local frame to a North-East-Down (NED) coordinate frame. Up to 48 different frame configurations can be corrected for [see '48 orientations.png'for more information].
- **Algorithm Selection**: Choose between the "standard" Euler angle method or the "SAAM" quaternion method for computation.
- **Offsets for Pitch, Roll, and Yaw**: These optional inputs (`pitch.offset`, `roll.offset`, `yaw.offset`) can be used to adjust for known offsets in the sensor's alignment with the body.
- **Plotting**: Set `plot = TRUE` to visualize corrected magnetometer data, including intermediate transformations.

### Outputs

Depending on input configurations, the function outputs may include:

- **Normalized Tri-axial Static Acceleration Data**: Expressed in the animal's body frame (`NGbx`, `NGby`, `NGbz`).
- **Calibrated Magnetometer Data**: Both raw and normalized data are expressed in the body frame (`Mx`, `My`, `Mz` and `NMbx`, `NMby`, `NMbz`).
- **Tilt-Corrected Magnetometer Data**: (`NMbfx`, `NMbfy`, `NMbfx`) if using `method = "standard"`.
- **Quaternion Outputs**: `q.w`, `q.x`, `q.y`, `q.z` for unitary (normalized) quaternion representation, if using the "SAAM" method.
- **Pitch, Roll, Yaw**: Angles describing the orientation of the animal's body, where Yaw is also referred to as heading (range: 0 to 360 degrees).
- **Plots**: Summary plots of correction procedures, available if `plot = TRUE` and method is not 0.

### Required Packages

- **rgl**: Required for 3D visualization and plots of corrected magnetometry data.

### Methodology References

- **Method 1**: Winer (2017). Simple and Effective Magnetometer Calibration.
- **Methods 2-8**: Vitali (2016). Ellipsoid or Sphere Fitting for Sensor Calibration.


## License

This project is licensed under the MIT License - see the `LICENSE` file for details.

## Contact

For questions or suggestions, feel free to contact me at [rgunner@ab.mpg.de].
