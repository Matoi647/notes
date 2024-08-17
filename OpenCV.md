### OpenCV 数据类型

OpenCV 使用 numpy 数组 (ndarray) 存储图像，通道为 BGR

若 dtype 为 np.float32，则数据范围为 [0, 1]，可以使用 imshow 显示图片，单无法使用 imwrite 保存图片

若 dtype 为 np.uint8，则数据范围为 [0, 255]，可以使用 imshow 显示图片，可以使用 imwrite 保存图片

保存图片时只能使用 np.uint8，视频也是。（且视频要求保存时将单通道转为 BGR 格式，图片不需要）

``` python
# depth.dtype: float32
# range: [0, 1]
# `imshow` works, `imwrite` doesn't
depth = cv2.normalize(depth, None, 0, 1, cv2.NORM_MINMAX)
depth = cv2.cvtColor(depth, cv2.COLOR_GRAY2BGR)
cv2.imshow('depth', depth)
if cv2.waitKey(30) & 0xFF == ord('q'):
    break
cv2.imwrite(os.path.join(output_dir, f'{i}.png'), depth)

# depth.dtype: uint8
# range: [0, 255]
# `imshow` works, `imwrite` also works
depth = cv2.normalize(depth, None, 0, 255, cv2.NORM_MINMAX)
depth = np.uint8(depth)
depth = cv2.cvtColor(depth, cv2.COLOR_GRAY2BGR)
cv2.imshow('depth', depth)
if cv2.waitKey(30) & 0xFF == ord('q'):
    break
cv2.imwrite(os.path.join(output_dir, f'{i}.png'), depth)
```

视频保存时要求将单通道转为 BGR，图片不需要

``` python
depth = cv2.normalize(depth, None, 0, 255, cv2.NORM_MINMAX)
depth = np.uint8(depth)
cv2.imshow('depth', depth)
if cv2.waitKey(30) & 0xFF == ord('q'):
    break
cv2.imwrite(os.path.join(output_dir, f'{i}.png'), depth)  # works
output_video.write(depth)   # doesn't work

depth = cv2.normalize(depth, None, 0, 255, cv2.NORM_MINMAX)
depth = np.uint8(depth)
depth = cv2.cvtColor(depth, cv2.COLOR_GRAY2BGR)
cv2.imshow('depth', depth)
if cv2.waitKey(30) & 0xFF == ord('q'):
    break
cv2.imwrite(os.path.join(output_dir, f'{i}.png'), depth)  # works
output_video.write(depth)   # works
```
