# Q&A
<table>
    <tr>
        <th>编写日期</th>
        <th>作者</th>
    </tr>
    <tr align="center">
        <td>2018.06.11</td>
        <td>鸡哥</td>
    </tr>
</table>

- **Q(6.4)：FPS player是否有一个碰撞代理(collision proxy/collider)？**
 
  **A**:是，unity里面的一个fps controller sample是用一个带物理属性的胶囊体(capsule)来模拟人物，从而实现上斜坡、跳等动作。
- **Q(6.6)：camera能否需要绑定在人物模型的头上？（例如扔手榴弹的时候头可能会移动，如果camera绑定在头上的话，会影响camera移动）**
 
  **A**：？？？（有人来回答一下吗）
- **Q(6.6)：在使用Timeline系统的时候，玩家能不能在timeline播放预设的实时渲染动画时（如字幕、骨骼动画）自行控制？（像使命召唤里面，NPC该干嘛干嘛，玩家自己是可以自己移动的）**
 
  **A**：似乎是可以的，因为timeline其实相当于一种预设的播放脚本，例如在第5秒A人物播放动画1，理论上不会影响玩家的移动。（隽元负责尝试一下）
- **Q(6.11)：是否要实现checkpoint系统？（在SubSceneStateController的状态转移时，存一下各种对象的状态？在服务端还是客户端？然后restore？）**
 
  **A**：A.别了吧，我tm还真没想到哪个pve是可以返回上一个检查点的。而且，在多人pve时checkpoint究竟实在客户端还是服务端储存数据呢？在服务端还要忍受网络IO，在客户端可能大家状态可能有点不同。<font color=red> **还是hardcore一点，死一个玩家就游戏结束返回房间！**<font color=black>