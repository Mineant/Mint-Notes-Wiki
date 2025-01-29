## 描述

Mint Notes 是一款可视化的板子软件。用户可以创建节点、节点之间的连接、图像和 JCards。JCard 是一种具有用户自定义字段的卡片。用户可以创建具有自定义名称、标题和文本字段的 JCard 模板。例如，一个名为“角色”的 JCard，默认标题为“新角色”，文本字段的默认值为：“生命值：0”，“防御：0”，“技能：无”。用户可以从模板生成 JCard 实例。用户可以修改实例的标题和文本字段。例如，在创建一个名为“角色”的 JCard 实例后，用户可以将标题修改为“英雄”，文本字段修改为“生命值：10”，“防御：10”，“技能：斩击”。JCard 旨在帮助用户快速创建和原型化卡牌游戏。图像也可以包含在 JCards 中。用户可以将整个 JCard 类型导出为 Excel，使所有 JCard 实例成为 CSV 表中的一行数据。此外，用户还可以导入 CSV 表格以生成 JCards。

## 软件设计

Mint Notes 使用 Unity C# 开发，采用 MVC 结构。模型作为数据库存储各种信息，例如 BoardModel 用于存储板子内的所有数据，NodeModel、ConnectionModel、JCardInstanceModel 等用于不同类型的信息。BoardController 包含 BoardModel，其他类可以通过 BoardController 修改板子模型。控制器之间经常相互交互。BoardController 还接收来自 BoardView 的回调，并处理 UI 的更新。视图和模型之间不会直接连接。

### 卡牌游戏模式

在卡牌游戏模式下，您可以创建不同版本的卡牌，称为 JCardInstances。这些卡牌最初在普通编辑模式下创建，您可以定义属性，如“生命值”和“防御”。例如，您可能有一个名为“英雄”的 JCardInstance，其初始生命值为 100。在卡牌游戏模式下，您可以为这些卡牌创建特定于游戏玩法的修改版本。

为此，引入了一种名为 CardGameJCardInstance 的卡牌类型。它基于原始的 JCardInstance，但允许在卡牌游戏模式中进行自定义。您可以修改文本字段，例如将生命值更改为 20。

为了处理模式之间的切换，您使用了一个名为 ModelUIReference 的可脚本化对象。它保存了卡牌不同 UI 预制件的引用。BoardView 使用 ModelUIReference 来确定每张卡牌使用哪个预制件。默认情况下，它在普通编辑模式下使用常规的 JCardInstance 预制件。当切换到卡牌游戏模式时，您更新 ModelUIReference，以使用 CardGameJCardInstance 预制件。

这种方法保持了系统的模块化和灵活性。您可以轻松地通过创建卡牌的附加版本并相应地更新 ModelUIReference 来添加更多模式。通过这种实现，您可以无缝地在模式之间切换，为卡牌游戏模式创建修改版本的卡牌，并确保使用正确的 UI 预制件。

## 为什么我想制作这款软件？

- 大多数可视化板子软件需要每月付费，否则功能有限。这款应用只需一次性付款。
- 纸质原型无法按比例创建。
  - 问题：创建卡牌的重复副本很麻烦。需要制作一个存储所有卡牌数据的表格，卡牌成为表格行的引用。查找数字不直观且耗时。
    - 解决方案：创建普通模式和卡牌游戏模式。在卡牌游戏模式中，可以从普通模式的卡牌创建卡牌实例。普通模式的卡牌更改将自动反映在卡牌游戏模式的卡牌实例中。
    - 重写卡牌实例以打破与普通模式卡牌之间的链接，这样您可以在卡牌游戏模式中随意编辑此卡牌。
  - 问题：一次性更改多个卡牌的值，如增加所有卡牌的伤害 1 点，耗时较长，因为每张卡牌都需要更改。
    - 解决方案：支持将卡牌的强大导入和导出到 CSV 表格。首先将卡牌导出到表格，然后使用 CSV 编辑软件（如 Excel / Google Sheets）批量编辑卡牌。然后将编辑后的表格导入回板子。导入支持保留或覆盖相同 ID 的原始卡牌，使导入过程非常灵活。
  - 问题：尽管在纸质原型中，您可以随意自定义卡牌，但卡牌空间有限，因此当无法再添加更多内容时，您需要擦除它。不断擦除耗时较长。
    - 解决方案：为卡牌添加许多可自定义选项，包括：名称、颜色、徽章、图标、框架、图像。
- 没有简单的方法来玩其他人制作的自定义卡牌游戏。
  - 问题：在纸质原型中，您可以随意自定义卡牌，但卡牌空间有限，因此当无法再添加更多内容时，您需要擦除它。不断擦除耗时较长。
- 当前的卡牌游戏模拟器过于复杂。
  - 问题：最著名的竞争对手：桌面模拟器，支持非常复杂的设计。然而，控制看起来不直观，宣传片是关于破坏游戏而不是创建游戏，3D 控制对某些人来说很复杂。
    - 解决方案：仅使用 2D UI 创建卡牌游戏模拟器。对计算机不太熟悉的人可以在 2D 中移动对象。
    - UI 简单但美观。采用极简风格，受到人们的喜爱。
- 多功能可视化板子软件，帮助进行一般设计工作。
  - 问题：我以前使用 Milanote 做笔记，它有许多出色的功能，如干净的 UI、简单的控制，但仍然缺乏我想要的一些功能。
    - （弱点：功能不足）解决方案：创建一款具有更多功能的可视化板子应用，包括：卡牌（可用于类图、游戏物品设计、任何需要多次创建的固定输入对象）、容器、卡牌徽章、轻松排列卡牌在网格中，调整卡牌的宽度等。
- （实现了多人功能）很少有卡牌游戏模拟器具备上述特性。



---

# Eng Ver

## Description

Mint Notes is a visual board software. The user can create nodes, connection between nodes, images, and JCards. Jcard is a type of card that has user defined fields. The user can create JCard templates with custom name, title, text fields. For example, a "Character" name JCard with a default title of "New Character", with text fields with default values: "Health: 0", "Defense: 0", "Skill: NA". The user can then generate a JCard instance from the template. The user can modify the title, and text fields of the instance. For example, after creating a "Character" JCard instance, the user can modify the title to "Hero", and text fields to "Health: 10", "Defense: 10", "Skill: Slash". JCard is meant for users to create and prototype card games quickly. Images can also be included in JCards. The user can export an entire JCard type to excel, making all JCard instances become a row of data in a csv table. And the user can import csv tables to become JCards. 



## Software Design

Mint Notes uses Unity c# to develop. It uses a MVC structure. Models act as a database for stuffs, for example there is BoardModel to store all the data inside a board, and NodeModel, ConnectionModel, JCardInstanceModel etc for different type of information. The BoardController contains the BoardModel, and other classes can access the BoardController to modify the board model. Controllers often interact with eachother. The BoardController also receives callbacks from the BoardView, and handles the update of the UI. The View and the Model will not connect with eachother.



### Card Game Mode

In the Card Game Mode, you can create different versions of cards called JCardInstances. These cards are initially created in Normal Edit Mode, where you define properties like "Health" and "Defense". For example, you might have a JCardInstance called "Hero" with an initial health value of 100. In the Card Game Mode, you can create modified versions of these cards specifically for gameplay.

To achieve this, you introduce a separate type of card called CardGameJCardInstance. It's based on the original JCardInstance but allows customization within the Card Game Mode. You can modify text fields like changing the health value to 20.

To handle switching between modes, you use a scriptable object called ModelUIReference. It holds references to different UI prefabs for the cards. The BoardView uses the ModelUIReference to determine which prefab to use for each card. By default, it uses the regular JCardInstance prefab for Normal Edit Mode. When you switch to Card Game Mode, you update the ModelUIReference to use the CardGameJCardInstance prefab instead.

This approach keeps the system modular and flexible. You can easily add more modes in the future by creating additional versions of the cards and updating the ModelUIReference accordingly. With this implementation, you can seamlessly switch between modes, create modified versions of cards for the Card Game Mode, and ensure that the correct UI prefabs are used.

## Why did I want to make this software?

- Most visual board software require a monthly payment, or else it has a limited functionality. This app just requires a one-time payment.
- Paper prototyping cannot create up to scale.
  - Problem: Creating cards duplicates of the same card is bothersome. A table that stores all the cards' data needs to be made, and cards become just references to the table's row. Looking up numbers is not intuitive and very time consuming.
    - Solution: Created a Normal Mode and Card Game Mode. In Card Game Mode, You can create Card Instances from cards in Normal Mode. Changes to cards in normal mode will automatically reflect on Card Instances from Card Game Mode.
    - Override a Card Instance to break its link between the card in normal mode, so you can edit this card in Card Game Mode how ever you like.
  - Problem: Changing many cards' value at once, like increasing all cards' damage by 1, takes a lot of time, since each cards needs to be changed.
    - Solution: Support robust import and export of cards to CSV Tables. First export the cards into a table, then use csv editing software like excel / google sheets to edit cards in mass. Then import the edited table back to the board. Importing supports keeping or overriding the original card with the same Id, making the importing process very customizable.  
  - Problem:  Although in Paper Prototyping, you can customize cards however you want, but a card has limited space, so when you cannot add more things to the card, you need to erase it. Constant erasing takes much time.
    - Solution: Add many customizable options to a card. Including: Name, Color, Badge, Emblem, Frame, Image
- There is not a easy way to play other people's custom made card game. (USG)
  - Problem: After
- Current card game simulators are too complicated. 
  - Problem: The most famous competitor: Table-top simulator, supports very complicated design. However, the controls looks not intuitive, the trailer is about destroying games instead of creating games, and 3D controls is complicated for some people.
    - Solution: Just use 2D ui to create a card game simulator. People less familiar with computers, can move objects around in 2D. 
    - The UI is simple but beautiful. Going for a minimalistic style, which people like.
- Multi-purpose visual board software, that helps with general design stuff.
  - Problem: I use Milanote for my notes before, it has many amazing features, like clean UI, simple controls, but it still lacks some functionality that I want.
    - (Weak: Not enough extra functionality) Solution: Create a visual board app that has more functionality. Including: Cards (usable for class diagrams, game item design, any type of object with fixed sets of input that needs to be create multiple times), Containers, Emblems for cards, arranging cards in a grid easily, adjust cards' width, and much more.
- (Multiplayer Function Implemented) There is very few card game simulators with the above characteristics.



### 1. Encouraging Creativity and Expression

Mint Notes empowers users to express their ideas and creativity by simplifying the design process. With an intuitive platform that removes barriers to entry, individuals of all skill levels can visualize and bring their concepts to life without frustration or intimidation. This accessibility encourages users to explore their creative potential and experiment with new ideas, ultimately enhancing their overall satisfaction and fulfillment in the creative process.

### 2. Enhancing Collaboration and Community

Mint Notes fosters teamwork and community engagement by enabling users to create and share custom card games easily. This feature promotes social interaction and strengthens bonds among users, as they collaborate on projects and share their creative endeavors. By making collaboration more accessible and enjoyable, Mint Notes cultivates a vibrant community of creators who can learn from one another and enhance their collective creative experiences.

### 3. Saving Time and Reducing Stress

By streamlining the card creation and modification process, Mint Notes helps users save time and reduce the mental load associated with managing multiple prototypes. The software’s user-friendly design allows for efficient modifications, eliminating the tedious aspects of traditional prototyping. Additionally, its affordable one-time payment model alleviates financial strain, enabling users to focus more on their creative pursuits rather than costs. This combination of efficiency and affordability allows users to engage more fully in their creative projects, leading to a more enjoyable and productive experience overall.