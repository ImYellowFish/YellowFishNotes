# View Space to Clip Space
## OpenGL

* near plane -> -1
* far plane -> 1
* Clip space range is \[0,far\](D3D-like) or \[-near,far\](OpenGL-like)

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;cot\theta&space;/R&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;cot&space;\theta&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;\frac{F&plus;N}{N-F}&space;&&space;\frac{2FN}{N-F}\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;cot\theta&space;/R&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;cot&space;\theta&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;\frac{F&plus;N}{N-F}&space;&&space;\frac{2FN}{N-F}\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} cot\theta /R & 0 & 0 & 0\\ 0 & cot \theta & 0 & 0 \\ 0 & 0 & \frac{F+N}{N-F} & \frac{2FN}{N-F}\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

where R is the width height ratio; theta is FOV/2

## D3D with reversed z
* near plane -> 1
* far plane -> 0
* D3D clip space coord is from 0(near) to 1(far). However recent D3D renders use reversed depth, so matrix z component is reversed in Unity shaders.
* Clip space range is [near,0]
* [Ref: Clip depth and clip range differences](https://docs.unity3d.com/Manual//SL-PlatformDifferences.html)

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;cot\theta&space;/R&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;cot&space;\theta&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;\frac{N}{F-N}&space;&&space;\frac{FN}{F-N}\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;cot\theta&space;/R&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;cot&space;\theta&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;\frac{N}{F-N}&space;&&space;\frac{FN}{F-N}\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} cot\theta /R & 0 & 0 & 0\\ 0 & cot \theta & 0 & 0 \\ 0 & 0 & \frac{N}{F-N} & \frac{FN}{F-N}\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

# U3D builtin parameters
## ProjectionParams
* _ProjectionParams.x: -1 on U3D for Y flip
* (C#)GL.GetGPUProjectionMatrix(Camera.projectionMatrix) = (Shader)UNITY_MATRIX_P if _ProjectionParams.x = 1
* (C#)GL.GetGPUProjectionMatrix(Camera.projectionMatrix) = (Shader)UNITY_MATRIX_P with flipped Y(_22) if _ProjectionParams.x = -1
* (C#)Camera.projectionMatrix = (Shader)unity_CameraProjection

## ViewSpace:
* ViewPos.z range: (-near, -far)

## ClipSpace
* ClipPosition.z: (D3D reversed-z) 1 to 0; (OpenGL) -1 to 1

## DepthMap
* DecodeDepthNormal depth: 0(near) to 1(far); depth = -viewPos.z / farplane
* SAMPLE_DEPTH_TEXTURE D3D RZ: 1(near) to 0(far) Nonlinear; OpenGL: 0(near) to 1(far) Nonlinear;
* [Ref: Linearize depth equations](http://www.humus.name/temp/Linearize%20depth.txt)
* Unity LinearEyeDepth param range: (0, 1)(D3D, OpenGL) or (1, 0)(D3D with reversed z)
* Unity LinearEyeDepth: near(near plane) to far(far plane) (positive value, regardless of platforms)
* Unity Linear01Depth: near/far(near plane) to 1(far plane) (regardless of platforms)