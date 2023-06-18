<h1>Crime Alias<img align="right" src="image.png" width="100px"></h1>
Crime alias that handles court records for criminals.

## Owner(s):
- Me (ShadowsStride)

# Current Plans:
- Potentially add additional images for the alias for variety.

## Help:
`!crime [player_name] [character_name]

In order to run this properly, you need to do the following:
- Create a server variable containing the records called `crime_dict`

### Crime Dictionary Variable
This server variable uses a json in order to work properly. The dictionary has keys of player's names, with the values being a dictionary containing crime data. Here is an example

```json
{
    "Shadow": {
        "Zylee Azuregrove": [["Robbery", 1000], ["Homicide", 50000]], "Bob": [["Loitering", 8000]]
    },

    "Bomber": {
        "Julie": [["Because I said so", 1000000]]
    }
}
```

For each player it uses the following properties:
- character (dict): Dictionary holding crime data
    - Crime (list): List holding crime name and crime cost
        - crime_name (str): Name of crime
        - crime_cost (int): Amount of gold the crime cost (think Skyrim bounty)

Here is a template that you can use:
```json
{
    "Player 1": {
        "Character 1": [["crime", 0], ["crime", 0]], "Character 2": [["Loitering", 8000]]
    },

    "Player 2": {
        "Character 1": [["crime", 0]]
    }
}
```

**UPDATING THIS SERVER VARIABLE**

You will need to run `!svar crime_dict` to copy over the previous settings before you update the server variable as it overwrites the existing data.

## Changelog:
6/16/2023 - Alias created

6/17/2023 - Documentation and [list](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/crime/list/list.md) alias has been created. Check the markdown file within the folde marked with their names for additional details.

## Copyright Notice

Copyright (C) Seth Hartman - All Rights Reserved.

THE CONTENTS OF THIS PROJECT ARE PROPRIETARY AND CONFIDENTIAL.
UNAUTHORIZED COPYING, TRANSFERRING OR REPRODUCTION OF THE CONTENTS OF THIS PROJECT, VIA ANY MEDIUM IS STRICTLY PROHIBITED.

The receipt or possession of the source code and/or any parts thereof does not convey or imply any right to use them
for any purpose other than the purpose for which they were provided to you.

The software is provided "AS IS", without warranty of any kind, express or implied, including but not limited to
the warranties of merchantability, fitness for a particular purpose and non infringement.
In no event shall the authors or copyright holders be liable for any claim, damages or other liability,
whether in an action of contract, tort or otherwise, arising from, out of or in connection with the software
or the use or other dealings in the software.

Abbreviations of the above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.