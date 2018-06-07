# Recoil设计

|       编写日期 | 作者      |
| ---------: | ------- |
| 2018.06.07 | ojf1996 |



## 目的

recoil类的目的，是为射击提供后坐力的模拟，从而增强游戏的真实感体验



## 数据成员

```c#
    //每秒开枪数量
    public int fireRate;

    //==================================================================
    //===================   枪支控制部分 ================================
    //==================================================================

    //我们希望通过一个水平位置的往复运动和一个垂直方向上的旋转来拟合枪支在连续/
    //单发状态下的后座。基本思路：在枪支的局部坐标系中，设置水平运动和垂直运动的终点。
    //在连续帧时，通过计算距离上一枪的时间，进行插值的方式实现连续的移动。
    //枪机初始位置
    public Vector3 gunInitPos;

    //枪机最大后摇位置
    public Vector3 gunShakePos;

    //枪机最大上摇欧拉角
    public Vector3 maxGunShake;

    //枪击初始欧拉角
    public Vector3 initGunEuler;

    //一枪完整时间
    private float timeOfOneShot;

    //枪支后摇最大的时间
    private float timeOfFullyRecoil;

    //枪支回复时长
    private float timeOfSteady;


    //==================================================================
    //===================   镜头控制部分 ================================
    //==================================================================

    //我们通过一个类似垂直上抛的运动来模拟镜头的后座，每一次开枪都会赋予镜头一个
    //向上的动量mv，然后在类似重力的作用力的作用下，镜头总是有回归初始位置的趋势量g。
    //有mv >= ∑g。

    //上下摆动的边界值
    public float minimumVert = 0.0f;
    public float maximumVert = 45.0f;

    //每一帧回归量g
    public Vector3 g;

    //一次上抬的动量
    public Vector3 mv;

    //剩余的动量，当leftMV > 0 才进行补偿，使得子弹回归，使得枪支总是上抬
    private float leftMV = 0;
```





## 提供接口

### public Vector3 getCurrentGunPos(float lastShot)

lastShot是指距离上一次开枪的时间。我们将一次开枪分为3个阶段：开枪瞬间，开枪后摇，开枪前摇，根据lastShot决定当前枪支移动的状态，然后根据lastShot和timeOfOneShot等值的关系，进行插值计算，得到枪支的位移量。



### public Vector3 getCurrentGunEuler(float lastShot)

基本原理和public Vector3 getCurrentGunPos(float lastShot)一致



###public Vector3 getCurrentGunEuler(float lastShot)

我们只有在开第一枪（即lastShot==0）时返回mv模拟剧烈的上抬，在一次开枪的其余阶段都返回g补偿上抬（当leftMv < 0时返回0，避免越打越低），当lastShot>一次开枪的最短时间(即不是连发)，就返回0。



## 使用接口

在RayShoter（可以为理解为GameController）中，先进行射击，计算上一次开枪时间

```c#
void Update()
    {
        if (Input.GetMouseButtonDown(0) || (Input.GetMouseButton(0) && fireMode != kindOfFireMode.SINGLE))
        {
            //在射速允许内，可以开火
            if (intervalFromLastShot >= intervalBetWeenTwoShot)
            {
                //归零
                intervalFromLastShot = 0.0f;
                //开火
                fire();
            }
        }
        //计算偏移
        pos_ = recoil.getCurrentGunPos(intervalFromLastShot);
        euler_ = recoil.getCurrentGunEuler(intervalFromLastShot);
        //处理玩家输入
        handleInput();
        //下一个开枪的阶段
        intervalFromLastShot += Time.deltaTime;
    }
```

在lateUpdate更新位置，实现后座

```c#
//更新武器与相机的相对位置，使得武器出现在屏幕的固定位置
weapon.transform.position = _camera.transform.TransformPoint(WeaponPos);
//添加offset，进行局部的位移，实现武器的前后抖动
weapon.transform.position = weapon.transform.TransformPoint(pos_);
//更新武器的旋转姿态
weapon.transform.rotation = _camera.transform.rotation * GunToCam;
//使得武器上摇
weapon.transform.Rotate(euler_);
```







### 







