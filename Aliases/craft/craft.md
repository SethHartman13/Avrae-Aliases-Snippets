<h1>Crafting Alias<img align="right" src="./images/image.png" width="100px"></h1>

Alias that handles the main functions of starting and continuing crafting sessions.

## Owner(s):
- Seth Hartman (ShadowsStride)

## Help:
`!craft <item_name> <item_category> <item_type/cost> <-s skill> <-b #> <eadv/adv/dis> <-i>`

- `item_name*`: Name of the item being crafted. Reminder: Use quotation marks for multi-word items.
- `item_category*`: Name of the category.
- `item_type/cost*`: If the category selected is not a cost-based category, name of the type. Otherwise, cost of the item.
- `-s skill_name`: - `-s skill_name`: This tells the crafting alias to use a skill modifier of the name given. (This is retained item to item, `-s ""` to clear skill)
- `eadv/adv/dis`: Applies double advantage/advantage/disadvantage.
- `-i`: Ignores training cooldown (DO NOT USE EXCEPT WHEN TOLD BY AN ADMIN).

*Only is used when starting to craft a new item

## Settings:

[settings.jsonc](settings.jsonc) is an example file as to what settings you can setup for your server (If you copy and paste, remember to remove comments, which is anything after //, otherwise Avrae will throw a parsing error). If you do not have a svar named `crafting_settings`, then it will turn to default settings (which are found at [settings.jsonc](settings.jsonc)).

### Item Categories:

Categories are symbolized by the main dictionary key within the settings svar. Some examples are the `common` and `nonmagical` item categories. There are two kinds of item categories: `type-based` and `cost-based` categories. Cost-based categories use numbers as their keys and type-based use names as their keys.

#### Type-Based

Settings:
```json
{
    "permanent": {
        ["Level Requirement (int)", "DC (int)", "Nat1 Penalty (int)", "Nat20 Bonus (int)", "Total Successes (int)", "Total Failures Allowed (int)", "Cooldown In Seconds (int)", "Retail Item Cost in GP (int or float)", "Hex code (with or without #)"]
    }
}
```

`Level Requirement`: Level required to craft the item type
`DC`: DC required to meet for success
`Nat1 Penalty`: Penalty to successes for a Nat1
`Total Successes`: Successes necessary to finish crafting the item
`Total Failures Allowed`: Maximum failures
`Cooldown In Seconds`: Cooldown between crafting sessions (3600 seconds is an hour)
`Retail Item Cost in GP`: Cost of item in GP (use decimal for costs that include copper and silver)
`Hex code`: Color code for embed card (set to "" for random color)

#### Cost-Based

Settings:
```json
{
    "0": {
        ["Level Requirement (int)", "DC (int)", "Nat1 Penalty (int)", "Nat20 Bonus (int)", "Total Successes (int)", "Total Failures Allowed (int)", "Cooldown In Seconds (int)", "Hex code (with or without #)"]
    }
}
```

`Level Requirement`: Level required to craft the item type
`DC`: DC required to meet for success
`Nat1 Penalty`: Penalty to successes for a Nat1
`Total Successes`: Successes necessary to finish crafting the item
`Total Failures Allowed`: Maximum failures
`Cooldown In Seconds`: Cooldown between crafting sessions (3600 seconds is an hour)
`Hex code`: Color code for embed card (set to "" for random color)

Using numbers as keys, they are thresholds on costs. I.e. If I try to craft a 5gp item, by default it goes past the 0gp threshold, but not the 101gp threshold.

Example:
```json
{
    "0": [5, 8, -1, 5, 1, 1, 7200, "#242528"],
    "101": [9, 13, -2, 5, 5, 2, 14400, "#242528"]
}
```

### General Settings
If you do not have the settings below, it does revert to default settings:

`lfg_integration`: This is a setting that works with the [LFG Alias](https://avrae.io/dashboard/workshop/6493acfad4ff5357d7b1cb32) I have written. All this does, is it will display a message with the LFG that the character is currently crafting. Default: False

`pro_rate_refund`: Whether or not the character gets a prorated refund if they decide to stop a project early. The prorated refund is calculated as followed:

```py
(1 - ((Number_of_Successes / Number_of_Successes_Needed) + (Number_of_Failures /(Number_of_Failures_Allowed * 2)))) * .5
```

Default: true

`success_dispType`: Display counter type for successes. Valid values:
- None
- "bubble"
- "square"
- "hex"
- "star"
Default: "star"

`failure_dispType`: Display counter type for failures. Valid values:
- None
- "bubble"
- "square"
- "hex"
- "star"
Default: "hex"

`jack_of_trades`: Whether or not Jack of All Trades applies to the crafting check. Default: true

`reliable_talent`: Whether or not Reliable Talent applies to the crafting check. Default: false

`success_mod_threshold`: The thresholds above the DC for additional successes. Default (don't forget to remove the comments, otherwise it will throw an error):

```json
{
    "-999": 1, // This key is always by default as meeting the DC always results in 1 success
    "5": 2, 
    "10": 3, 
    "15": 4, 
    "20": 5 // The highest key sets the maximum amount of successes possible (even with Nat20 bonuses)
}
```

`whitelisted_channel_ids`: This list allows staff to control what channels/threads craft commands (that alter the CCs in any fashion) are run in. You will need to grab the channel ID of each channel/thread you want whitelisted. If the list is empty, then it will allow all channels/threads. Default: []

`parent_channel_inherit`: This determines if threads of whitelisted channels inherit the whitelisted status. This is not recommended as this does not stop players from creating threads within channels and running commands without staff knowledge. Default: false

`xp_categories`: This determines if players get xp for finishing items. Category names need to match those setup, otherwise players will not receive xp. If the xp_categories is turned on, the subalias will add xp to xp tracker (recommended to use the [New XP](https://avrae.io/dashboard/workshop/618b77bd5c51fd18fe5356a0) library made by bryonius, otherwise it shows up in cvars). These are the valid input types:
- string (singular category or all categories):
    - Name of a single category i.e. `"common"`
    - `"all"`, will allow all categories
- list (singular category or selective categories):
    - `["category 1", "category 2", "category 3"]`
        - If `"all"` is a string in the list, it will allow all categories
- dictionary (selective types and categories):
    - `{"category 1": "all", "category 2": ["perm", "all"], "category 3": "perm"}`
        - If `"all"` is a value (either as a string or a string within a list), it will allow all item types within that category.
- boolean (true or false):
    - `true`, will act like `"all"`
    - `false`, does not give xp at all

Default: false

## Changelog:
7/31/2023 - Alias created with documentation

6/4/2023 - Added xp support

8/21/2023 - Documentation update. Added reliable talent functionality