# 三叉戟行动（Operation Trident）文档

### 目录
1. [头脑风暴](brainstorm/README.MD)（记录游戏开始制作前的想法）
2. [游戏策划](planning/game/README.MD)（剧情、关卡等详细设计）
3. [项目管理相关文档](planning/project/README.MD)
4. [会议记录](minutes/README.MD)（记录每次会议讨论的内容）
5. [开发教程](tutorial/README.MD)（实现某个内容的详细步骤，包含美工、程序？）
6. [开发文档](development/README.MD)（开发之间沟通所需的文档）
7. [文档规范](CONTRIBUTING.MD)**（更新文档前先看！！！）**

## Q&A
### 2018.06.04

> - **Q: FPS player是否有一个碰撞代理(collision proxy/collider)？**  
> - A: 是，unity里面的一个fps controller sample是用一个带物理属性的胶囊体(capsule)来模拟人物，从而实现上斜坡、跳等动作。

### 2018.06.06

> - **Q: camera能否需要绑定在人物模型的头上？（例如扔手榴弹的时候头可能会移动，如果camera绑定在头上的话，会影响camera移动）**
> - A: ？？？？？？？

> - **Q: 在使用Timeline系统的时候，玩家能不能在timeline播放预设的实时渲染动画时（如字幕、骨骼动画）自行控制？（像使命召唤里面，NPC该干嘛干嘛，玩家自己是可以自己移动的）**
> - A（隽元）: 似乎是可以的，因为timeline其实相当于一种预设的播放脚本，例如在第5秒A人物播放动画1，理论上不会影响玩家的移动。（隽元负责尝试一下）

### 2018.06.11
> - **Q：是否要实现checkpoint系统？（在SubSceneStateController的状态转移时，存一下各种对象的状态？在服务端还是客户端？然后restore？）**
> - A：别了吧，我tm还真没想到哪个pve是可以返回上一个检查点的。而且，在多人pve时checkpoint究竟实在客户端还是服务端储存数据呢？在服务端还要忍受网络IO，在客户端可能大家状态可能有点不同。<font color=red> **还是hardcore一点，死一个玩家就游戏结束返回房间！**<font color=black>