<h1>Training Alias<img align="right" src="image.png" width="100px"></h1>

Training alias that allows players to train in various proficiencies. Allows for customization of training settings. This does take into account Fey Wanderer Ranger's ability to add their wisdom modifier to charisma ability checks. You can also manage what proficiencies players can learn and what ability score is used for each.

This does require cvar `subclass` to contain `Fey Wanderer`, otherwise the bonus will need to be manually done.

## Owner(s):
- Me (ShadowsStride)

## Current Plans:
- None

## Help:
`!train <prof_name> <-b> <adv/dis> <i>`

`prof_name`: If the training has not started prof_name is required. If continuing training you do not add it.

`-b`: Adds bonus to check.

`-i`: Ignores training cooldown (DO NOT USE EXCEPT WHEN TOLD BY AN ADMIN, the alias does keep track if this was used).

`adv`/`dis`: Applies advantage/disadvantage.

## Settings
- [General](#settings-dictionary-variable)
- [Tools](#tool-settings-dictionary)
- [Languages](#language-settings-dictionary)
- [Weapons](#weapon-settings-dictionary)
- [Instruments](#instrument-settings-dictionary)
- [Gaming Sets](#gaming-set-settings-dictionary)
- [Skills README](#skill-settings-dictionary-readme)
- [Armor REAMDE](#armor-settings-dictionary-readme)

### Settings Dictionary Variable
The `training_settings` server variable uses a json to customize the settings with training. This is not required, instead it will use default values. Here are the following settings:

- max_val: Integer that sets the max number of successes necessary - relevant ability score (i.e. 10 - CharismaMod (+3) = 7 successes) Default: 10

- disp_type: Shows what kind of counter type is shown, here are the following options:
  - None
  - "bubble"
  - "square"
  - "hex"
  - "star" (default)

- jack_of_trades: Says whether or not Jack of All Trades is used in the ability check.
  - 1: True (default)
  - 0: False

- thresholds: Determines how many successes you get based upon what you roll. By default, any roll below 10 constitutes as 0 successes, 10-19 is 1 success, and 20+ is 2 successes.
  - {"-999": 0, "10": 1, "20": 2}

- time_cooldown: Determines how often someone can train in seconds. By default, the cooldown is 65000 seconds (6.5 days).

[Example Dictionary](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/train/dictionary%20examples/settings.json)


### Tool Settings Dictionary
This server variable uses a json to determine what tool proficiencies can be learned and what ability scores are used for each. Within the `tool_dict` svar, any tools left out of the svar will become tools that players are not allowed to learn through the training alias.

If you do not have the `tool_dict` svar created, it will default to the below settings:

[Dictionary Example](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/train/dictionary%20examples/tools.json)

|                         | Strength | Dexterity | Intelligence | Wisdom | Charisma |
|:-----------------------:|:--------:|:---------:|:------------:|:------:|:--------:|
|   Alchemist's Supplies  |          |           |       X      |    X   |          |
|    Brewer's Supplies    |          |           |       X      |    X   |     X    |
| Calligrapher's Supplies |          |     X     |       X      |        |     X    |
|    Carpenter's Tools    |     X    |     X     |       X      |    X   |          |
|     Cobbler's Tools     |     X    |     X     |       X      |    X   |     X    |
|       Cook's Tools      |          |     X     |       X      |    X   |          |
|   Glassblower's Tools   |          |     X     |       X      |        |          |
|     Jeweler's Tools     |          |     X     |       X      |        |     X    |
|  Leatherworker's Tools  |     X    |     X     |              |    X   |          |
|      Mason's Tools      |     X    |           |       X      |        |          |
|    Painter's Supplies   |          |     X     |              |    X   |     X    |
|      Potter's Tools     |          |     X     |              |    X   |          |
|      Thieves' Tools     |          |     X     |       X      |        |          |
|      Tinker's Tools     |          |     X     |       X      |        |          |
|      Weaver's Tools     |          |     X     |       X      |    X   |          |
|    Woodcarver's Tools    |          |     X     |       X      |    X   |          |
|      Smith's Tools      |     X    |     X     |              |        |          |

### Language Settings Dictionary
This server variable uses a json to determine what languages can be learned and what ability scores are used for each. Within the `lang_dict` svar, any languages left out of the svar will become languages that players are not allowed to learn through the training alias.

If you do not have the `lang_dict` svar created, it will default to the below settings:

[Dictionary Example](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/train/dictionary%20examples/languages.json)

|             | Intelligence | Wisdom | Charisma |
|:-----------:|:------------:|:------:|:--------:|
| Abanasinian |       X      |    X   |     X    |
|   Abyssal   |       X      |    X   |     X    |
|    Aquan    |       X      |    X   |     X    |
|    Auran    |       X      |    X   |     X    |
|  Celestial  |       X      |    X   |     X    |
|   Daelkyr   |       X      |    X   |     X    |
| Deep Speech |       X      |    X   |     X    |
|   Draconic  |       X      |    X   |     X    |
|   Dwarvish  |       X      |    X   |     X    |
|    Elvish   |       X      |    X   |     X    |
|    Ergot    |       X      |    X   |     X    |
|    Giant    |       X      |    X   |     X    |
|     Gith    |       X      |    X   |     X    |
|   Gnomish   |       X      |    X   |     X    |
|    Goblin   |       X      |    X   |     X    |
|   Hadozee   |       X      |    X   |     X    |
|   Halfling  |       X      |    X   |     X    |
|    Ignan    |       X      |    X   |     X    |
|   Infernal  |       X      |    X   |     X    |
|   Istarian  |       X      |    X   |     X    |
| Kenderspeak |       X      |    X   |     X    |
|  Kharolian  |       X      |    X   |     X    |
|     Khur    |       X      |    X   |     X    |
|   Kothian   |       X      |    X   |     X    |
|    Kraul    |       X      |    X   |     X    |
|    Leonin   |       X      |    X   |     X    |
|   Lexodon   |       X      |    X   |     X    |
|  Marquesian |       X      |    X   |     X    |
|   Minotaur  |       X      |    X   |     X    |
|    Naush    |       X      |    X   |     X    |
|   Nerakese  |       X      |    X   |     X    |
| Nordmaarian |       X      |    X   |     X    |
|     Ogre    |       X      |    X   |     X    |
|     Orc     |       X      |    X   |     X    |
|  Primordial |       X      |    X   |     X    |
|    Quori    |       X      |    X   |     X    |
|   Reidran   |       X      |    X   |     X    |
|   Solamnic  |       X      |    X   |     X    |
|    Sylvan   |       X      |    X   |     X    |
|    Terran   |       X      |    X   |     X    |
|  Thri-kreen |       X      |    X   |     X    |
| Undercommon |       X      |    X   |     X    |
|   Vedalken  |       X      |    X   |     X    |
|   Zemnian   |       X      |    X   |     X    |

### Weapon Settings Dictionary
This server variable uses a json to determine what weapons can be learned and what ability scores are used for each. Within the `weapon_dict` svar, any weapons left out of the svar will become weapons that players are not allowed to learn through the training alias.

If you do not have the `weapon_dict` svar created, it will default to the below settings:

[Dictionary Example](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/train/dictionary%20examples/weapons.json)

|                | Strength | Dexterity |
|:--------------:|:--------:|:---------:|
|      Club      |     X    |           |
|     Dagger     |     X    |     X     |
|    Greatclub   |     X    |           |
|     Handaxe    |     X    |           |
|     Javelin    |     X    |           |
|  Light Hammer  |     X    |           |
|      Mace      |     X    |           |
|  Quarterstaff  |     X    |           |
|     Sickle     |     X    |           |
|      Spear     |     X    |           |
|      Yklwa     |     X    |           |
| Light Crossbow |          |     X     |
|      Dart      |          |     X     |
|    Shortbow    |          |     X     |
|      Sling     |          |     X     |
|    Battleaxe   |     X    |           |
|      Flail     |     X    |           |
|     Glaive     |     X    |           |
|    Greataxe    |     X    |           |
|   Greatsword   |     X    |           |
|     Halberd    |     X    |           |
|      Lance     |     X    |           |
|    Longsword   |     X    |           |
|      Maul      |     X    |           |
|   Morningstar  |     X    |           |
|      Pike      |     X    |           |
|     Rapier     |     X    |     X     |
|    Scimitar    |     X    |     X     |
|   Shortsword   |     X    |     X     |
|     Trident    |     X    |           |
|    War Pick    |     X    |           |
|      Whip      |     X    |     X     |
|     Blowgun    |          |     X     |
|  Hand Crossbow |          |     X     |
| Heavy Crossbow |          |     X     |
|     Longbow    |          |     X     |
|       Net      |     X    |           |

### Instrument Settings Dictionary
This server variable uses a json to determine what instruments can be learned and what ability scores are used for each. Within the `instrument_dict` svar, any instruments left out of the svar will become instruments that players are not allowed to learn through the training alias.

If you do not have the `instrument_dict` svar created, it will default to the below settings:

[Dictionary Example](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/train/dictionary%20examples/instruments.json)

|               | Strength | Dexterity | Constitution | Intelligence | Wisdom | Charisma |
|:-------------:|:--------:|:---------:|:------------:|:------------:|:------:|:--------:|
|    Bagpipes   |          |           |              |       X      |        |     X    |
|      Drum     |          |           |              |       X      |        |     X    |
|    Dulcimer   |          |           |              |       X      |        |     X    |
|     Flute     |          |           |              |       X      |        |     X    |
|      Lute     |          |     X     |              |       X      |        |     X    |
|      Horn     |     X    |           |              |       X      |        |     X    |
|   Pan Flute   |          |           |              |       X      |        |     X    |
|     Shawm     |          |           |              |       X      |        |     X    |
|      Lyre     |          |     X     |              |       X      |        |     X    |
|      Viol     |          |     X     |              |       X      |        |     X    |
|   Bird Pipes  |          |           |              |       X      |        |     X    |
|     Glaur     |          |           |       X      |              |        |     X    |
|   Hand Drum   |          |     X     |              |              |        |     X    |
|    Longhorn   |          |           |              |              |    X   |     X    |
|    Songhorn   |          |           |              |       X      |        |     X    |
|     Tantan    |          |     X     |              |              |        |     X    |
|    Thelarr    |          |           |              |       X      |        |     X    |
|     Tocken    |          |     X     |              |              |        |     X    |
|    Wargong    |     X    |           |              |              |        |     X    |
| Whistle-stick |          |           |              |              |    X   |     X    |
|    Yarting    |          |     X     |              |              |        |     X    |
|    Zulkoon    |          |           |       X      |              |        |     X    |

### Gaming Set Settings Dictionary
This server variable uses a json to determine what gaming sets can be learned and what ability scores are used for each. Within the `gaming_dict` svar, any gaming sets left out of the svar will become gaming sets that players are not allowed to learn through the training alias.

If you do not have the `gaming_dict` svar created, it will default to the below settings:

[Dictionary Example](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/train/dictionary%20examples/gaming.json)

|                       | Dexterity | Intelligence | Wisdom | Charisma |
|:---------------------:|:---------:|:------------:|:------:|:--------:|
|        Dice Set       |     X     |       X      |    X   |     X    |
|    Dragonchess Set    |           |       X      |    X   |     X    |
|    Playing Card Set   |     X     |       X      |    X   |     X    |
| Three-dragon Ante Set |           |       X      |    X   |     X    |

### Skill Settings Dictionary (README)
This server variable uses a json to determine what skills can be learned. This is **NOT** RAW. 

If you do not have the `skill_dict` svar created, it will be (by default) turned off.

[Dictionary Example](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/train/dictionary%20examples/skills.json)

### Armor Settings Dictionary (README)
This server variable uses a json to determine what skills can be learned. This is **NOT** RAW. 

If you do not have the `armor_dict` svar created, it will be (by default) turned off.

[Dictionary Example](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/train/dictionary%20examples/armor.json)

## Changelog
- 9/20/23
  - Skill proficiencies are now turned off by default.
  - Armor proficiencies have been added, they are turned off by default
  - Moved proficiency dictionaries into the alias itself, no longer dependent upon GVARs