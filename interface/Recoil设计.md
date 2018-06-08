# Recoil设计
<table>
    <tr>
        <th>更新日期</th>
        <th>作者</th>
    </tr>
    <tr>
        <td align="center">2018.06.08</td>
        <td align="center">ojf1996</td>
    </tr>
</table>

## 目的

recoil类的目的，是为射击提供后坐力的模拟，从而增强游戏的真实感体验



## 数据成员

```c#
    //一枪的时间
    public float intervalOfShoot;

    //枪支初始位置
    private Vector3 gunInitPos = Vector3.zero;

    //枪支后摆最大位置
    public Vector3 gunEndOffset = Vector3.left;

    //枪支初始上抬角度
    private Vector3 gunInitEulerAngle = Vector3.zero;

    //枪支摆动最大角度
    public Vector3 gunEndEulerAngle = Vector3.right; 

    //一枪的时间段的分割点
    public float divideFactor = 0.3f;

    //镜头上抬最大角度
    public float camMaxEulerInX;
    public float camMaxEulerInY;

    //当前枪支位置
    private Vector3 mCurrentGunPos = Vector3.zero;

    //当前枪支上抬角度
    private Vector3 mCurrentGunEulerAngle = Vector3.zero;

    //当前相机上抬角度
    private float mCurrentCameraEulerAngleInXAxis = 0.0f;

    //当前相机左右摆角度
    private float muCurrentCameraEulerAngleInYAxis = 0.0f;
```





## 提供接口

### public IEnumerator DoGunRecoilCycle()

协程，用于初始化枪支的抖动



### public IEnumerator DoCamRecoilCycle()

协程，用于初始化镜头抖动



###public float GeCameraEulerAngleInYsAxis()

获取镜头的水平方向的偏移量



### public float GetCameraEulerAngleInXAxis()

返回镜头垂直方向的偏移量



### public Vector3 GetGunEulerAngle()

返回枪支抖动时的上抬角度



### public Vector3 GetGunPos()

返回枪支抖动前后移动的offset



## 使用接口

先调用 DoGunRecoilCycle，DoCamRecoilCycle（可在update中）

```c#
void Update()
{
     StartCoroutine(recoil_m.DoGunRecoilCycle());
     StartCoroutine(recoil_m.DoCamRecoilCycle());
}
```

在lateUpdate更新位置，实现后座

```c#
Vector3 gunPos = recoil_m.GetGunPos();
Vector3 gunEuler = recoil_m.GetGunEulerAngle();
float camEulerInX = recoil_m.GetCameraEulerAngleInXAxis();
float camEulerInY = recoil_m.GetCameraEulerAngleInYAxis();
```





## 补充

假如只调用DoCamRecoilCycle一次，得到的offset将会从0变化到camMaxEulerInX，再从

camMaxEulerInX变化到0.

假如在调用一次DoCamRecoilCycle之后继续调用DoCamRecoilCycle，得到的offset值将会是一个从0持续变大，但是总是会最后变为0的值。



### 







