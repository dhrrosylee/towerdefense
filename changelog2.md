！！！每一次的changelog都在对应的压缩包内，在此再上传一次方便老师和助教检查！！！

5月30日

今日变化总览：Tower和Card结构微调，增加资源累积功能

#change

合并card和tower

卡片底座本质是事先放置好的图片

而卡片上的塔与种在地图上面的塔本质上没有区别。

#add

tower类

tower 的析构函数    ~Tower();

设置塔的种类    void setType(int type);   主要是图片和高级普通炮塔之分

后续增加血条和升级功能
还有死掉功能
哦还有发射子弹

#delete

card类：把设置属性放到了tower里面，card就删了 void setTowerIndex(int index)函数

#add

card类

mGold：种下塔需要花费的金钱    void setGold(int gold)

相应的，card的初始化列表加入mGold

且设置画笔在塔的下方提醒玩家买塔多少钱，好像大了。有点影响画面美感，先这样吧，有空再改

增加资源积累功能

玩家生命值    mPlayerHealth

玩家金币值    mPlayerGold                    

卡片的金币值    mCardGold

并绘制到playscene：PlayScene::drawPlayerInfo(QPainter *painter)

能不能买得起塔

    Card *findCard(int type)

    bool canBuyCard(Card *card)
#
#
#
6月2日
主要变动：增加monster类配置怪物属性，并在屏幕上走动

怪物的属性有：

1.是不是boss，bool mBoss;

2.int mGold;值多少钱

3.double mSpeed; 速度void setSpeed(double speed);

4.QPixmap mCachePixmap;长什么样void setType(int type) 随机配置不同样子的怪物
图片随机轮回，因为懒和时间原因，只做了两种怪物。
boss和normal，序号大于20的是boss的图片，小于等于20的怪物是normal

playscene：void setSceneIndex(int index)改为void loadScene(int index)加载场景

setSceneIndex功能不变，只是加入了startgame（）等函数，加载完场景开始游戏

向Playscene写入怪物向量

后面别忘了要增加血条！！！！
#
#
#
6月4日
主要变动：增加monster类配置怪物属性，并在屏幕上走动

怪物的属性有：

1.是不是boss，bool mBoss;

2.int mGold;值多少钱

3.double mSpeed; 速度void setSpeed(double speed);

4.QPixmap mCachePixmap;长什么样void setType(int type) 随机配置不同样子的怪物
图片随机轮回，因为懒和时间原因，只做了两种怪物。
boss和normal，序号大于20的是boss的图片，小于等于20的怪物是normal

怪物自身有update（）

向Playscene加入怪物向量，怪物生成计时器，帧率计时器

playscene：void setSceneIndex(int index)改为void loadScene(int index)加载场景

setSceneIndex功能不变，只是加入了startgame（）等函数，加载完场景开始游戏

一进入startgame怪物生成计时器，帧率计时器就开始了

加入怪物生成函数void generateMonster();

向Playscene构造函数加入定时器

加入updateObjects()函数，更新物体信息

startgame以后过几秒就生成怪物

但是感觉电脑跑不动，得缓冲一下
#
#
#
6月6日

主要改动：增加缓冲绘图，处理怪物边界

#add

QPixmap mBuffer，加入playscene里

加入drawToBuffer()函数，怪物，塔，背景，玩家信息，拖动的塔都放进去

loadScene(int index)最初的加载场景绘制到缓冲区

把updateObjects() 函数里的东西绘制到缓冲区

#add

增加GameHelper类，刷新率问题

class GameBorder处理怪物走到边界

class Time把刷新率放进来了
#
#
#
6月8日

主要改动：给怪物和塔装载血条，怪物增加攻击力打塔

属性：继承qobject类

目前的生命值     currentHealth

最大生命值    maxHealth

二者都初始化为10

有以下四个函数

Blood(QObject *parent = nullptr);

void copyOther(const Blood &other);

virtual Blood *duplicate() const;

virtual void draw(QPainter *painter);

塔和怪物增加属性：mBlood

增加函数    void enableBlood(bool enable)          血条显示
#
#
#
6月10日

主要变动，实现怪物打塔

怪物增加攻击力：mAtk

为了简便，怪物打塔的方式直接变成，碰到塔就消失，塔掉血

怪物撞塔死掉    void death(Monster *monster);

塔受伤        Tower::takeDamage(int damage)

塔没血gg       void death(Tower *tower)

在playscene里面写入碰撞函数collidingObjects()

updateObjects（）里面加入碰撞处理函数
#
#
#
6月12日

设置boss

怪物类里加入setBoss（）

速度是normal的0.7

金钱是20

攻击力是10，一碰塔，塔就没了

修改setType：主要是改图片大于20的图片是boss，其他的是normal

Playscene里面加入boss生成时间

修改startGame()函数，游戏开始2分钟后boss出现

boss是否死掉->是否成功的标志

修改collidingObjects()函数，boss碰到塔，塔就没了，boss还可以继续走

#
#
#