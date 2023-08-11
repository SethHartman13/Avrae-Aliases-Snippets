<h1>Crime Alias<img align="right" src="image.png" width="100px"></h1>
Crime alias that handles court records for criminals.

## Owner(s):
- Me (ShadowsStride)

## Current Plans:
- None

## Help:
`!crime [player_name] [character_name]`

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

6/17/2023 - Documentation and list subalias has been created. Check the markdown file within the folder marked with their names for additional details.

6/17/2023 - Subalias help has been created. Check the markdown file within the folder marked with their names for additional details.

6/22/2023 - Copyright/License Update

7/4/2023 - Alias rewrite

8/11/2023 - Depreciated list subalias, rewrote alias