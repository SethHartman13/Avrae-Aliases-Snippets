<h1>Rep Alias<img align="right" src="image.png" width="100px"></h1>

Reputation alias that handles reputation with organizations and groups.

## Owner(s):
- Me (ShadowsStride)

## Current Plans:
- None

## Help:
`!rep [organization] <#>`
[]'s imply required argument, <>'s imply optional argument

In order to run this properly, you need to do the following:
- Create a server variable for each organization (i.e. Renown)
- Create a server variable containing the name of the svars for each organization called `org_list`

### Organization Server Variable
This server variable uses a json in order to work properly. It uses the "name" property to identify the name of the organization. And it uses numbers to identify reward thresholds. It also has a place to put an url for an icon for the organization, if not filled out, it defaults to the icon shown in the top right corner of this markdown file. Here is an example:
```json
{"name": "Renown", "10":["10x10 Plot of Land"], "15": ["Jacket of Speed"], "20": ["10x20 Plot of Land"], "25": ["Jacket of Swiftness"], "30": ["20x20 Plot of Land"], "35": ["Jacket of Speedy Bois"], "imgurl": "www.someimage.png"}
```

For each "threshold," you need to have the key be a string and the value to be a list of strings. i.e. the threshold is 10 and the items you can get at reputation level 10 is Jelly Beans and Cotton Candy:

```"10": ["Jelly Beans", "Cotton Candy"]```

Here is template that you can use:
```json
{"name": "Name of org", "10":[""], "15": [""], "20": [""], "25": [""], "30": [""], "35": [""], "imgurl": ""}
```

### Organization List Server Variable
This server variable uses a json in order to work properly. You must use the svar name ***org_settings*** You can set the key values to be anything (as long as there are no duplicates), but I recommend using numbers in ascending order (as strings). The values closer to the beginning of the json will be checked first. Here is an example:
```json
{"1": "renown_settings", "2": "uni_fed_settings", "3": "potato_uni_settings"}
```

For each organization name, you will need to have it match the name of the server variable you created up in [Organization Server Variable](#organization-server-variable). If you named the server variable for the Renowned as "RenRep" then you need to insert "RenRep" in the Organization List server variable.

Here is a template that you can use:
```json
{"1": "Organization 1 svar", "2": "Organization 2 svar", "3": "Organization 3 svar"}
```

**UPDATING THIS SERVER VARIABLE**

You will need to run `!svar org_settings` to copy over the previous settings before you update the server variable as it overwrites the existing data.

## Changelog:
6/6/2023 - Subaliases [list](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/rep/list/list.md), [rewards](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/rep/rewards/rewards.md), and [help](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/rep/help/help.md) have been created. Check the markdown files within the folders marked with their names for additional details.

6/6/2023 - Added notes to help, teaching optional versus required arguments.

6/8/2023 - Copyright notice and image added.

6/8/2023 - Added template jsons for svars.

6/14/2023 - Updated copyright notice

6/22/2023 - Copyright/License Update

6/27/2023 - Improved dictionary algorithm and UI update

## License Notice

This work includes material written by Seth Hartman (aka ShadowsStride) and is licensed under the Creative Commons Attribution 4.0 International License available at https://creativecommons.org/licenses/by/4.0/legalcode.