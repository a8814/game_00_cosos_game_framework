# cocos游戏基础框架

### 适用范围
适用于新手，包含一些基础的游戏界面、逻辑、内容管理。

### 文件说明
- [AppMain] 游戏启动唯一主入口，资源载入、初始化本地存储、loading界面逻辑管理
- [G] 通用方法
- [L] 本地存储方法
- [MPanel] 界面管理，每一个界面独立成为一个prefab，每次需要打开时载入
- [MRes] 资源管理，动态载入resource下的资源
- [MSoud] 声音管理
- [GamePlay] 游戏的主Gameplay
- [tools/] 常用工具类脚本，脚本命名方式为T*
    - [i18n/MLanguage] 多语言
    - [TAddPrefab] onLoad()时添加一个prefab
    - [TChildNode] 子节点管理
    - [TNull] 空脚本
    - [TSize] 节点比例化修改大小
    - [TZIndex] 编辑器中修改节点zIndex
    - [TSimpleFSM] 简单状态机调度
    - [TErase] 橡皮擦效果
- [panel/] 界面脚本，脚本命名方式为Panel*，本项考虑prefab命名的关系，不进行命名简化
    - [PanelWait] 一个通用的等待页面
    - [PanelGuide] 一个个人使用的新手引导页面
    - [PanelMessage] 一个通用的消息页面
- [anima/] 动画脚本，脚本命名方式为Anima*，本项考虑到动画/粒子的特殊性，不进行命名简化
    - [AnimaNumber] 数字变动动画
- [system/] 子系统脚本，脚本命名方式为S*
- [controller/] 游戏内重要组件的控制器，脚本命名方式为C*

### 两层逻辑设计（尽量使得逻辑扁平话，少分层，多分模块）：System+Controller
1. System层，包含游戏主逻辑（GamePlay）和各子系统（System）
    * 主要实现游戏逻辑（可以理解成不同组件的操作集合），比如过关逻辑（next_level）就包含清理数据，场景切换，加分动画等子逻辑。
    * 子系统则用来实现除游戏主逻辑外的额外逻辑，例如：新手引导系统、离线奖励系统等。
    * 子系统根据控制子逻辑的多少分成3类：对应0个Panel的子系统，如数值系统；对应1个固定Panel的子系统，如离线奖励系统；对应多个不固定Panel的子系统，如分数系统、收集系统等。
    * 对应1个固定Panel的子系统，如离线奖励系统，进行脚本简化，将系统脚本（S*）合并到界面脚本中（Panel*）。
2. Controller层，包含界面的控制器（Panel）和各界面中重要组件的控制器（Controller）