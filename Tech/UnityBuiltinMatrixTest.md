# Camera Setup
* FOV = 60
* NearPlane = 1
* FarPlane = 100
* Width/Height = 1.819905

<br><br>
# OpenGL Core

## Calculation

By the OpenGL projection matrix formula:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;cot\theta&space;/R&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;cot&space;\theta&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;\frac{F&plus;N}{N-F}&space;&&space;\frac{2FN}{N-F}\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;cot\theta&space;/R&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;cot&space;\theta&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;\frac{F&plus;N}{N-F}&space;&&space;\frac{2FN}{N-F}\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} cot\theta /R & 0 & 0 & 0\\ 0 & cot \theta & 0 & 0 \\ 0 & 0 & \frac{F+N}{N-F} & \frac{2FN}{N-F}\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

We have:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;-1.0202&space;&&space;-2.0202\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;-1.0202&space;&&space;-2.0202\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} 0.9517 & 0 & 0 & 0\\ 0 & 1.732 & 0 & 0 \\ 0 & 0 & -1.0202 & -2.0202\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

## unity_CameraProjection (Shader)

Same as the calculated matrix.

## MainCamera.projectionMatrix (C#)

Same as the calculated matrix.

## GL.GetGPUProjectionMatrix (C#, Not RenderTexture)

Same as the calculated matrix.

## GL.GetGPUProjectionMatrix (C#, RenderTexture)

Same as the calculated matrix.

## glstate_matrix_projection (Shader, UNITY_MATRIX_P)

Same as the calculated matrix.


<br><br>
# Direct3D 11 (Reversed z)

## Calculation

By the D3D projection matrix formula:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;cot\theta&space;/R&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;cot&space;\theta&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;\frac{N}{F-N}&space;&&space;\frac{FN}{F-N}\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;cot\theta&space;/R&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;cot&space;\theta&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;\frac{N}{F-N}&space;&&space;\frac{FN}{F-N}\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} cot\theta /R & 0 & 0 & 0\\ 0 & cot \theta & 0 & 0 \\ 0 & 0 & \frac{N}{F-N} & \frac{FN}{F-N}\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

We have:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} 0.9517 & 0 & 0 & 0\\ 0 & 1.732 & 0 & 0 \\ 0 & 0 & 0.0101 & 1.0101\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

However to get the right result in Unity, the Y component needs to be negated.
The right matrix to use in rendering is:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;-1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;-1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} 0.9517 & 0 & 0 & 0\\ 0 & 1.732 & 0 & 0 \\ 0 & 0 & 0.0101 & 1.0101\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

## unity_CameraProjection (Shader)

Same as OpenGL projection matrix.

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;-1.0202&space;&&space;-2.0202\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;-1.0202&space;&&space;-2.0202\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} 0.9517 & 0 & 0 & 0\\ 0 & 1.732 & 0 & 0 \\ 0 & 0 & -1.0202 & -2.0202\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

## MainCamera.projectionMatrix (C#)

Same as OpenGL projection matrix.

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;-1.0202&space;&&space;-2.0202\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;-1.0202&space;&&space;-2.0202\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} 0.9517 & 0 & 0 & 0\\ 0 & 1.732 & 0 & 0 \\ 0 & 0 & -1.0202 & -2.0202\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

## GL.GetGPUProjectionMatrix (C#, Not RenderTexture)

Same as the calculated matrix with positive Y. Will give wrong result.

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} 0.9517 & 0 & 0 & 0\\ 0 & 1.732 & 0 & 0 \\ 0 & 0 & 0.0101 & 1.0101\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

## GL.GetGPUProjectionMatrix (C#, RenderTexture)

Same as the calculated matrix with negative Y. Will give the right result.

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;-1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;-1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} 0.9517 & 0 & 0 & 0\\ 0 & -1.732 & 0 & 0 \\ 0 & 0 & 0.0101 & 1.0101\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

## glstate_matrix_projection (Shader, UNITY_MATRIX_P)

- OnRenderImage, before Blit

Same as the calculated matrix with negative Y.

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;-1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;-1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} 0.9517 & 0 & 0 & 0\\ 0 & -1.732 & 0 & 0 \\ 0 & 0 & 0.0101 & 1.0101\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

- OnRenderImage, after Blit

Same as the calculated matrix with positive Y. During Blit call, the matrix y component is negated for handling renderTexture.

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} 0.9517 & 0 & 0 & 0\\ 0 & 1.732 & 0 & 0 \\ 0 & 0 & 0.0101 & 1.0101\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

- OnPostRender

After the rendering process, the y component is restored.

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;-1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{Bmatrix}&space;0.9517&space;&&space;0&space;&&space;0&space;&&space;0\\&space;0&space;&&space;-1.732&space;&&space;0&space;&&space;0&space;\\&space;0&space;&&space;0&space;&&space;0.0101&space;&&space;1.0101\\&space;0&space;&&space;0&space;&&space;-1&space;&&space;0&space;\end{Bmatrix}" title="\begin{Bmatrix} 0.9517 & 0 & 0 & 0\\ 0 & -1.732 & 0 & 0 \\ 0 & 0 & 0.0101 & 1.0101\\ 0 & 0 & -1 & 0 \end{Bmatrix}" /></a>

<br><br>
# Test

In vertex shader, we use different matrices mentioned above to transform the vertex into projection space.
Then we compare the result to the original scene.

The tested matrices are:

1. Internal MVP (original)
2. Internal MVP with negated Y (original, modified)
3. UNITY_MATRIX_P (before Blit)
4. unity_CameraProjection
5. GL.GetGPUProjectionMatrix, renderToTexture = false
6. GL.GetGPUProjectionMatrix, renderToTexture = true
7. Internal MVP then unity_CameraInvProjection then unity_CameraProjection
8. Internal MVP then unity_CameraInvProjection then UNITY_MATRIX_P

The second testcase is to illustrate the impact of negative Y. Not only the positions are changed,
but the cull result is impacted too. You need to toggle the cull mode to Cull Front to get the same faces.

Specially, we add the last testcase to validate the use of the unity_CameraInvProjection matrix to transfrom from clip-space to view-space.

## Result: OpenGL Core

Basically all the matrices are the same, so they will yield the same result, except testcase 2.

## Result: Direct3D 11 (Reversed z)

Correct testcases:
1 = 3 = 6 = 7

Inverted Y:
2 = 5

Inverted Y and wrong Z:
4 = 8

It is worth noting that, when using unity_CameraInvProjection to transform pos from clip-space to view-space,
the Y component of the view pos is negated. Also the z component will be wrong. By applying the wrong matrices two times, we get the correct clip-space pos again, but the intermediate view pos cannot be trusted, unless handled specially on D3D platforms.

![alt text][result]

[result]: ./md_image/UnityBuiltinMatrixTest.jpg "Result"