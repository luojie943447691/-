# 一、相机 Camera
## 1.1 分类
[说明连接](https://blog.csdn.net/qq_43607777/article/details/115758549)
### 1.1.1 PerspectiveCamera：透视相机，最接近自然的视图，符合近大远小的规律。
![[Pasted image 20220723182920.png]]

![[Pasted image 20220723182652.png]]

### 1.1.2  **OrthographicCamera**：正交相机，所有事物渲染一样大，开发二维游戏时常用这种。
![[Pasted image 20220723183455.png]]
![[Pasted image 20220723183507.png]]

## 1.2 相机位置(.position)和相机拍摄位置(.lookAt())
相机Camera的基类是Object3D,相机对象camera具有位置属性.position，通过位置属性.position可以设置相机的位置。

.lookAt()方法用来指定相机拍摄对象的坐标位置，.lookAt()方法的参数是表示位置坐标的三维向量对象Vector3，所以.lookAt()方法的参数可以通过代码new THREE Vector3(x, y, z)设置。实际开发的时候，你希望相机对准哪个对象，就返回那个对象的位置属性.position，比如scene.position， 就表示返回场景scene的位置坐标，如果把scene.position换成某个网格模型对象的位置就是mesh.position，mesh.position表示网格模型mesh的本地位置坐标。通过相机观察点的位置和.lookAt()方法指向的位置就可以计算出相机的拍摄角度,本质上就是计算出相机对象的视图矩阵.matrixWorldInverse。

对于透视投影而言，相机位置与lookAt指向的观察目标位置间隔距离越小，场景中的三维模型放大倍数越大，准确地说是透视投影相机可以拍摄的范围更小，同时场景scene中超出的相机参数约束范围的部分会被剪裁掉。
![[Pasted image 20220724104940.png]]


