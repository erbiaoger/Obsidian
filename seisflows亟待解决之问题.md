- 1、mpi 问题

    * Mpi 正演没有问题

    - 反演时只能用 4 个

- 2、反演到底面，需要更改梯度更新步长，还是更改波持续时间Nt

    

    ![截屏2022-10-27 上午11.33.24](https://raw.githubusercontent.com/erbiaoger/PicGo/main/img202210271133607.png)

    

    

    

- 3、震源频率对反演的影响







- 4、line search 停止



实现均匀半空间模型的反演， 但只能迭代两次

![截屏2022-10-27 上午11.19.03](/Users/erbiaoger/Share/截图/截屏2022-10-27 上午11.42.42.png)



![img202210271120211](https://raw.githubusercontent.com/erbiaoger/PicGo/main/img202210271120211.png)



- 5、如果模型变小，比如480m * 100m 网格点数不变，也会报图片大小的错

    





- 6、如何将实测数据加入



