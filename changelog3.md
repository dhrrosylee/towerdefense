！！！每一次的changelog都在对应的压缩包内，在此再上传一次方便老师和助教检查！！！

#changelog

第三次

概览：1.完成子弹类
2.塔具有发射子弹功能
3.敌人碰到子弹死亡

！！！目前存在的bug，路上只要塔一种下去，就开始发射子弹不管路上有没有敌人

6.13-6.17
#add：bullet类
构造函数
explicit Bullet(QObject *parent = nullptr);

void copyOther(const Bullet &other);

virtual Bullet *duplicate() const Q_DECL_OVERRIDE;

virtual void update() Q_DECL_OVERRIDE;

double speed;                       移动速度
int damageValue;                  伤害值


在GameHelper类下面加入GameManager类，代表总的子弹
static QList<Bullet *> TotalBullet;

在monster类里
加入takeDamage（int damage）函数，用于承受伤害，受到伤害掉血
在monster构造函数得初始化列表中加入

塔类增加保护成员
子弹冷却时间             mCoolTime
子弹计时器                 mCoolTimer
还有一筐子弹             mBullet

在tower的构造函数初始化列表，初始化以上三个成员

在setType函数中加入damageValue（子弹攻击力），先都等于1吧
子弹路径之前设置好就不用管了
配置塔对应发射的子弹

在copyOther函数中加入mCoolTime，mCoolTime和mBullet的初始化

增加update（）函数，不断刷新，然后发射子弹，先所有的塔发射一种子弹吧

在塔的析构函数里加入，删除塔所对应的子弹

在PlayScene::updateObjects()里面更新物体信息加入子弹

在PlayScene::drawToBuffer()加入绘制子弹的操作

在PlayScene::clearAll()里加入清除所有子弹的操作

在PlayScene::collidingObjects()处理边界

首先子弹飞出场景，就删除子弹

然后处理怪物和子弹的碰撞，子弹碰到怪物消失，怪物受到伤害

测试成功！！

修改最后一排塔发射的子弹属性，一次可以发五个，朝四面八方射
即在update里面增加子弹旋转角度，和旋转增量
