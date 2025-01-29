# Mint Notes Documentation

## Description

Mint Notes is a visual board software. The user can create nodes, connection between nodes, images, and JCards. Jcard is a type of card that has user defined fields. The user can create JCard templates with custom name, title, text fields. For example, a "Character" name JCard with a default title of "New Character", with text fields with default values: "Health: 0", "Defense: 0", "Skill: NA". The user can then generate a JCard instance from the template. The user can modify the title, and text fields of the instance. For example, after creating a "Character" JCard instance, the user can modify the title to "Hero", and text fields to "Health: 10", "Defense: 10", "Skill: Slash". JCard is meant for users to create and prototype card games quickly. Images can also be included in JCards. The user can export an entire JCard type to excel, making all JCard instances become a row of data in a csv table. And the user can import csv tables to become JCards. 



## Software Design

Mint Notes uses Unity c# to develop. It uses a MVC structure. Models act as a database for stuffs, for example there is BoardModel to store all the data inside a board, and NodeModel, ConnectionModel, JCardInstanceModel etc for different type of information. The BoardController contains the BoardModel, and other classes can access the BoardController to modify the board model. Controllers often interact with eachother. The BoardController also receives callbacks from the BoardView, and handles the update of the UI. The View and the Model will not connect with eachother.



### Card Game Mode

In the Card Game Mode, you can create different versions of cards called JCardInstances. These cards are initially created in Normal Edit Mode, where you define properties like "Health" and "Defense". For example, you might have a JCardInstance called "Hero" with an initial health value of 100. In the Card Game Mode, you can create modified versions of these cards specifically for gameplay.

To achieve this, you introduce a separate type of card called CardGameJCardInstance. It's based on the original JCardInstance but allows customization within the Card Game Mode. You can modify text fields like changing the health value to 20.

To handle switching between modes, you use a scriptable object called ModelUIReference. It holds references to different UI prefabs for the cards. The BoardView uses the ModelUIReference to determine which prefab to use for each card. By default, it uses the regular JCardInstance prefab for Normal Edit Mode. When you switch to Card Game Mode, you update the ModelUIReference to use the CardGameJCardInstance prefab instead.

This approach keeps the system modular and flexible. You can easily add more modes in the future by creating additional versions of the cards and updating the ModelUIReference accordingly. With this implementation, you can seamlessly switch between modes, create modified versions of cards for the Card Game Mode, and ensure that the correct UI prefabs are used.
