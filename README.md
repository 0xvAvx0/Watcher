# Watcher
## 一个泰拉瑞亚tshock插件

## 功能介绍：

### 1. 能够对游戏内玩家行为的详细信息进行记录。
记录每个玩家手里拿着什么物品、丢弃什么物品、生成什么射弹（在有人炸图或乱喷腐化溶液的时候可以快速找到嫌疑人），均记录在Watcher文件夹内的logs里，玩家作弊信息记录在cheatlogs里。支持1.44中雪溶液和沙溶液的检测。

### 2. 多线钓鱼检测
支持对多线钓鱼的检测，包括1.44中新增的一堆钓鱼浮标饰品，并且能在配置文件中设置最多允许几线钓鱼（？赞成作弊？）

### 3. 射弹伤害检测
tshock自带射弹伤害检测，但是没有排除1.44中新增的升级版泰拉剑，永夜，真永夜，圣剑等特效武器的bug，这些武器在搭配可耻或传奇词缀或者玩家佩戴泰坦手套及上级合成物时会意外触发假高额伤害，尽管游戏里并不会伤害过高，但会被tshock的检测误判，这个功能的目的在于让你关掉tshock的射弹伤害检测，启用优化过的。

### 4. 物品作弊检测
新版本应用了新的算法，对游戏内所有敌怪的掉落物进行监督，若未击败过这种生物却获得了这个物品则算作弊。不可掉落的物品仍然按照以前的垃圾查找来鉴别是否作弊，总之更新物品检测范围更大了，也更精确了（不包括装饰性家具，画等），这会检测玩家的所有物品，包括猪猪，虚空袋，熔炉，保险箱，另外两套装备栏。
注意，敌怪掉落物检测依靠图鉴内容进行判定，任何非玩家友方npc杀死的敌人不会计入图鉴，同样也不算入击杀次数，如各种机关岩浆（这种生物你不会一次都没击杀过吧？）

### 5. 星璇机枪bug检测
如果你不打算让任何pe端的人进入你的服务器，那么这个功能没有任何作用。该功能可以把卡星璇机枪bug的玩家算入作弊。不知道什么是星璇机枪bug的可以去B站直接搜

### 6. 更高级的作弊统计
目前只有4钟作弊类型统计，如上四条，现在可以单独在配置文件中设置每种作弊类型的处理方式了
#### `"XX作弊是否计入总违规作弊次数": true,`
通过修改为true将违反这种检测的玩家塞入作弊名单，这会统计他们总共的作弊次数，false则不统计；
#### `"伤害作弊警告方式": 3,`
通过修改数值来决定惩罚方式：0 仅仅口头警告，发送两条私聊消息警告作弊玩家，1 玩家会被网住一段时间并发送广播警告，2 直接杀死玩家并发送广播消息警告，3 kick掉玩家，4 直接ban掉玩家；
#### `"最多违规作弊次数": 10,`
通过修改该值来决定最多违规作弊次数，当玩家总共作弊次数达到该值时，直接ban，若上一条警告方式直接设置为4，那么这个就没有意义了
#### 作弊玩家数据`CheatPlayers.json`
现将作弊玩家数据写入该文件钟，这个文件记录了玩家名称，uuid，违法了哪种作弊类型，总计作弊次数

### 7. 恶魔心饰品栏限制
tshock不会把恶魔心饰品栏的栏位数据保存在服务器，这导致玩家之间的饰品栏数目有差异，为了更公平，该功能启用后会强制在肉前将游戏内所有玩家恶魔心饰品栏里的饰品卸下来，该功能不算违规检测，属于一种强制执行。

### 8. 允许设置npc免受玩家伤害
顾名思义，相较于前版本功能被砍了，因为tshock更新后部分钩子不能使用，目前只能让生物免疫来自玩家的直接伤害，不能免疫debuff（以前是可以让任何生物免疫任何伤害）

### 9. 自动备份tshock.sqlite文件
原版tshock只备份了地图，sqlite文件没有备份，而又有极低的概率损坏玩家的存档。可设置备份时常间隔。不用担心日志过多，会自动清理，可改日志的备份时常，间隔，日志大小。


## 指令
- 权限1:【无，任何人都能使用】
- 指令1：/watcher help
- 功能1：查看该插件下的所有指令帮助
- 指令1-2：/watcher me
- 功能1-2：查看自己的违规情况
-
- 权限2： watcher.locknpc
- 指令2： /locknpc npc.id或boss名称或boss名称拼音缩写
- 功能2： 保护这个npc不会被伤害和杀死，管理员可以使用`/clear npc`来清除npc
-
- 权限3： watcher.unlocknpc
- 指令3： /unlocknpc npc.id或boss名称或boss名称拼音缩写
- 功能3： 移除受保护的npc
-
- 权限4： watcher.listlocknpc
- 指令4： /listlocknpc
- 功能4： 列出所有受保护的npc
-
- 权限5： watcher.adduncheckeditem
- 指令5： /adduci item.id
- 功能5： 该插件的物品作弊检查功能不会检查这个物品
-
- 权限6： watcher.delunchecheditem
- 指令6： /deluci item.id
- 功能6： 移除这个物品不会被检查的效果
-
- 权限7： watcher.listuncheckeditem
- 指令7： /listuci
- 功能7： 列出所有避免被检查的物品

## 用法
直接将插件放置于tshock插件文件夹里即可，默认修改控制台为中文，可改。

你可以在Watcher/logs文件夹里看到玩家日常信息搜集，在watcher/cheatlogs文件夹里看到作弊信息搜集，在Watcher/tshock_backups文件夹里看到备份的sqlite文件，在WatcherConfig.json里修改你需要的各种配置信息，在CheatPlayers.json里查看所有作弊玩家信息。

输入`/locknpc 46`那么所有的兔兔均不能被玩家直接杀死（debuff除外）。输入`/locknpc kslzy`或`/locknpc 克苏鲁之眼`或`/locknpc 4`或`/locknpc ky`或`/locknpc 克眼`那么克苏鲁之眼和克苏鲁之仆同理（对于boss，一次添加会同时保护boss和大多数boss的仆从，肢体等，这里`/locknpc 4`同时保护了克眼和仆从，对于机械骷髅王还会同时保护四个钳子，不需要用户一个一个输入指令来保护）

输入`/unlocknpc 46`将解除兔兔的保护，克眼也一样，同时解除boss的仆从，肢体保护

输入`/listlocknpc`来查看哪些npc被保护

输入`/adduci 2624`来将海啸设置为不被检查的物品，因为Watcher插件有物品进度检测功能，在打败猪鲨之前获得海啸会被认定为作弊，使用此指令将该物品设置为豁免物

输入`/deluci item.id`来移除某个物品的豁免

输入`/listuci`来查看所有豁免物品

## WatcherConfig.json

一个可以详细修改功能的文件，修改后在控制台或游戏内使用`/reload`即可生效，下面对每个项进行了解释
```
{
  "启用中文": true,                                             
  "是否备份tshockSql": true,                                                      
  "tshockSql备份间隔分钟": 20,                                                    
  "tshockSql备份时常分钟": 2880,                                                  
  "启用物品作弊检测": true,                                                       
  "单人物品检测概率": 0.4,                                                        //0.4即每次开始物品检测时有40%概率真的发生了检测
  "全员物品检测间隔时间秒": 400,                                                  //每隔一段时间对游戏内全员进行物品检测，范围 >0 的整数
  "不需要被作弊检查的物品ID": [],                                                 //在此处写入物品id，将不会对该物品检测
  "必须被检查的物品_覆盖上面一条": [],                                            //在此处写入物品id，必定检测，这个功能会覆盖上一条
  "物品作弊警告方式": 3,                                                          //检测到违规了进行的警告方式，详情看前面 更高级的作弊统计 部分
  "物品作弊是否计入总违规作弊次数": true,                                         //同上
  "启用射弹伤害检测": true,                                                       
  "射弹最大伤害": 3000,                                                           
  "伤害作弊警告方式": 3,                                                          
  "伤害作弊是否计入总违规作弊次数": true,                                          
  "启用浮标数目检测": true,                                                       
  "最大浮标数目": 1,                                                              //最多允许几个浮标钓鱼，如果是0就是禁止钓鱼，如果>1，那么。。。。你允许玩家自由作弊吗？
  "钓鱼作弊警告方式": 3,                                                          
  "钓鱼作弊是否计入总违规作弊次数": true,                                          
  "是否启用pe版星璇机枪bug检测": true,                                             
  "星璇机枪作弊警告方式": 3,                                                       
  "星璇作弊是否计入总违规作弊次数": true,                                          
  "是否禁用肉前恶魔心饰品栏": true,                                                
  "最多违规作弊次数": 10,                                                         //所有违规类型的总统计次数，超过该值直接ban
  "需要被检测的玩家组": [                                                         //游戏内所有检测功能会检测的对象，包括作弊检测，恶魔心检测
    "default",
    "vip"
  ],
  "被保护的NPC": [],
  "是否把对话内容写入日志": true,                                                //就是把正常玩家对话和使用指令写到watcher/logs里（不包含密码）
  "是否把丢弃物写入日志": true,                                                  //丢弃物包括正常丢弃和用户在世界进行操作时生成的物品，如砍树掉落的木头也算进去
  "是否把手持物写入日志": true,                                                  //顾名思义，这些已经写的很浅显易懂了
  "是否把生成射弹写入日志": true,
  "任何日志的备份时常分钟": 21600,
  "日志和作弊日志文件的最大MB": 5,
  "拿持日志中的豁免物品ID": [                                                    //当玩家手持这些物品时，不会写入日志，以防日志记录太多无效信息，这里2，3仅是例子，该插件会自动为你生成常用的豁免ID，无需手动搜集
    2,
    3
  ],
  "丢弃日志中的豁免物品ID": [                                                    //同上
    0,
    2
  ],
  "射弹日志中需要记录的危险的射弹物ID": [                                         //这里是需要记录的射弹，与上面的反过来了，通常这里是炸弹，岩浆炸弹，各种火箭等危险毁图射弹，该插件也已经准备好常用的警告射弹物ID了，这里的10，11仅是例子，无需手动搜集
    10,
    11
  ]
}
```

## 其他
- 物品检测两套算法，一套根据生物图鉴统计击杀数来判断是否物品为合法获得，另一个其实就是根据游戏进度，从统计好的数据里查，没有技术含量，由于泰拉物品太多并不能准确判断每个物品是否合理，插件还在缓慢更新，若有物品判断错误请将它加入豁免物里并及时反馈。若是用户使用特殊地图，地图里包含正常地图不应该存在的超进度物品，则需要用户注意，避免错误踢人，可以在豁免物里写入这些物品。
- 该插件日后缓慢更新

## 代码很烂请大佬不要在意，欢迎大家使用
