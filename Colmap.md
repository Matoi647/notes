# COLMAP, 3DGS(ply文件) 坐标系

COLMAP 使用 OpenCV 坐标系: x right, y down, z front

https://blog.csdn.net/OrdinaryMatthew/article/details/126670351

原始 3DGS 使用 COLMAP 坐标系，即 OpenCV 坐标系

https://github.com/graphdeco-inria/gaussian-splatting/issues/100#issuecomment-1686463391

gsplat 使用 OpenCV 坐标系

gsplat: https://github.com/nerfstudio-project/gsplat/issues/160#issuecomment-2040615000

supersplat 使用 PlayCanvas坐标系: x left, y up, z front

https://github.com/playcanvas/supersplat/issues/289#issuecomment-2478381611

# 相机外参, 相机位姿，viewmat, C2W, W2C

C2W: 将相机坐标系下的点坐标变换到世界坐标系，以世界坐标系为中心，等价于相机位姿

W2C: 将世界坐标系下的点坐标变换到相机坐标系，以相机坐标系为中心，等价于相机外参，viewmat

