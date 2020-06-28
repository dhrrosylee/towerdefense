！！！每一次的changelog都在对应的压缩包内，在此再上传一次方便老师和助教检查！！！


changelog4

概览：1.游戏开始前有倒计时，游戏失败和胜利场景
2.升级拆除功能

PlayScene中加入 enum GameState游戏状态

void setGameState(GameState state)设置游戏状态

void triggeredAction(QAction *action) 拆除和升级功能
bool checkSceneSuccess()  &&  bool checkGameOver()    检查是否成功或失败

QTimer *mLoadingTimer;                 倒计时
QMenu *mMenu;                               右键菜单
QAction *mDeleteAction;                   拆除
QAction *mUpgradeAction;               升级
int mLoading;                                    倒计时

在PlayScene构造函数里面加入倒计时
在缓冲绘图的里面绘制倒计时
在updateObjects（）函数里加入判断游戏是否结束或者开始
//检查当前场景是否结束，结束条件是 boss 死亡，并且怪物列表为空
加入PlayScene::checkSceneSuccess()函数，如果怪物都死光了，就成功了


修改contextMenuEvent事件，因为我是用右键菜单实现升级和拆除功能的，左边的塔升级成右边的塔
#bug

1.修改路上没有怪物也发射子弹的bug
在monster类里面加入怪物所在路径int road
在playscene里面加入每条路径上怪物个数

2.使高级塔不能直接建立在空地上

6.18

加入了音效，没有再添加cpp文件，因为我一添加include “music.h”我的monster的各种属性就乱了，就直接在playscene里面加了


6.23

子弹图片的尺寸改大了一倍，因为好看

塔加入的减速功能，就是在子弹的属性里加入了slowspeed，然后再playscene处理碰撞的时候，如果slowspeed不为0，就让monster的速度减去slowspeed

塔加入了增益功能，就是打到的怪物，打死后，金币会增加

塔加入了劝退功能，就是速度乘以-1

修改敌人还在出生地，被减速直接死亡的bug，劝退返回出生地才会死亡
