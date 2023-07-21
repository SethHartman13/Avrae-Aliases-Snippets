<h1>LFG Alias<img align="right" src="image.png" width="100px"></h1>

LFG Alias that allows players to look for a group to do a quest.

## Owner(s):
- Me (ShadowsStride)

## Current Plans
- Allow advantage to be displayed in passives (still needing to verify if possible)

## Settings Server Variable

This LFG alias allows you to customize what is being shown whenever a player runs the alias, if you do not alter any settings (or don't alter settings properly), they do have default values. Here are the different options:

- subclass
    - Default: On
    - This determines whether or not subclass is displayed or not alongside the character's class.
    - In order for this to work properly you need to do one of the following:
        - Subscribe to [Verbose Character Tools](https://avrae.io/dashboard/workshop/5f7385fe647bb0a416316d1d). Then run `!level sub ABC` (ABC is the sourcebook code, refer to `!help level` or the workshop site for codes). Then after that, run `!level class subclass`
        - Create a cvar named "subclass" and use the following template: `{classLevel: subclass, class2Level: subclass}`

- thp
    - Default: On
    - This determines whether or not temporary hit points are displayed with hp.

- img
    - Default: On
    - This determines whether or not the character's portrait (if any) is displayed as a thumbnail photo.

- player
    - Default: Off
    - This detemines whether or not the player is mentioned. Automatically changes if the player changes their display name.

- ac
    - Default: Off
    - This shows the character's AC.

- ins
    - Default: Off
    - Displays passive insight.
    - In order for observant to apply properly, you have to have a cvar named `feats` and have 'observant' in the cvar. Recommended to have [Verbose Character Tools](https://avrae.io/dashboard/workshop/5f7385fe647bb0a416316d1d) and run `!manage feats add observant`.

- inv
    - Default: Off
    - Displays passive investigation

- perc
    - Default: Off
    - Displays passive insight
    - In order for observant to apply properly, you have to have a cvar named `feats` and have 'observant' in the cvar. Recommended to have [Verbose Character Tools](https://avrae.io/dashboard/workshop/5f7385fe647bb0a416316d1d) and run `!manage feats add observant`.

- spell_list
    - Default: Off
    - Displays the entire spell list. This only works if the character has spells in the first place.

- spell_slot
    - Default: Off
    - Displays the available and used spellslots. This only works if the character has spells in the first place.

- full_subclass
    - Default: Off
    - Experimental
    - Displays the full wording of the subclasses. I.e. Oath of Conquest Paladin rather than just Conquest Paladin.
    - Requires subclasses to be enabled.

Here is an example dictionary with default values. You do not need every value, only values you want to change:

```json
{"subclass": 1, "thp": 1, "player": 0, "ac": 0, "ins": 0, "inv": 0, "perc": 0, "spell_list": 0, "spell_slot": 0, "full_subclass": 0}
```

## Changelog:

6/21/23 - Alias created

6/27/23 - Documentation completed

7/21/23 - Added support for automatic adv/dis (based upon character sheet)