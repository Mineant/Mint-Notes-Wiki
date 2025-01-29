# JCard Introduction

JCards are cards in the project. You can use them to create cards with custom fields. You can customize their type, text fields, icon, tags, symbols for different settings. Here are different ways of using the cards:



In a board game:

[Image with Character, Item, Building cards]



Class Diagram
[Image with Class and function cards]





# JCard Creation

Create from scratch

1. Open the normal board
2. Click "Create JCard" from the Object Creator Bar
3. Enter your card name, e.g. "Character"
4. Press "Create"



[insert image of the creating JCard Character]



The JCard Template Window should automatically open up after creating the card. We will talk about the functionality later. You can press "Exit" to exit for now.

Now you can see your card's icon has appeared on the Object Creator Bar. You can drag the icon to create a new JCard of that template.



# JCard Template

Here, you can set the template information for the JCard. Templates are basically the settings for every JCard. 

You can open the window, by clicking the JCard icon on the Object Creator Bar, then click "Edit Template".

Templates are basically what your JCard looks like when it is created. Each JCard created from a Template is called "JCard Instance". But we will call it "JCard" in this documentation. The Template will be called "JCard Template".

## Basic Settings

This panel are the Basic Settings. One the left are the setting fields, on the right you can preview the real time changes for the JCard.

- Card Type: Type of card, used for grouping cards into different categories, for example "Character", "Item", "Action".
- Nickname: Displayed at the Object Creator Bar, for easy to view purpose.
- Default Name: The default name for a JCard Instance when it is created.
- Emblem: A Icon for this JCard. Every JCard Instance from this Template will have the same Emblem.
- Expose Id Field: Every JCard has a id field, which is mainly used when you export and import JCards to CSV.
- Image: Enable to let JCard to have display images.
- Width: The default width.
- Custom Width: If enabled, every JCard will be able to have different widths. If not, every JCard's width is depend on the Width setting.
- Value Label: A small text field on the top right corner of the JCard.



## Textfield Settings

Click on the bottom bar to enter Textfield Settings.

You can modify the textfields shown on the JCard.

Press "New Textfield" to create a new textfield.

Click on the Name and Default Name of the respective fields to edit them.

The eye icon indicates the visibility of the field. Fields with no visibility, while it is not visible on the board, the data is still contained in the JCard.

You can click the area at the right side of the visibility icon to open the options for the text fields.

- Up/Down: Change the order of the text field
- Settings: Change the font style of this field (Not Implemented)
- Delete: Removes the TextField



# Tags and Symbols

You can add tags and symbols to JCards for more customization and categorization.

## Tags

### Tag Creation

Tags are text fields. For example, for character, you can create "Electric", "Ground", "Fire", and many different tags. JCards can equip none, or a infinite amount of tags.

1. Click Library
2. Enter Tag Name and Choose Color
3. Click Create

### Tag Edit

You can edit a tag after creating it. All the changes will be applied to all existing JCards.

1. Click Library
2. Click on a tag
3. Click Edit
4. Change the tag name or color

### Tag Equip

1. Click on Edit
2. Click the tags at the "Tags" window to equip to current JCard
3. Click the tags at the "Equipped" window to unequip to current JCard

## Symbols

Symbols are icons. The edit, equip, and creation process is very similar to the tags. Please reference the Tags Documentation. [Insert link to tags documentation]

# Import/Export

You can import a existing CSV to help you quickly create your JCards.

## Import

You can import a CSV to create a completely new JCard Template and its corresponding JCard Instances.



Show import

Then Export





