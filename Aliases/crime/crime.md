<h1>Crime Alias<img align="right" src="image.png" width="100px"></h1>
Crime alias that handles court records for criminals.

## Owner(s):
- Me (ShadowsStride)

# Current Plans:
- Potentially add additional images for the alias for variety.

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

6/17/2023 - Documentation and [list](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/crime/list/list.md) subalias has been created. Check the markdown file within the folder marked with their names for additional details.

6/17/2023 - Subalias [help](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/crime/help/help.md) has been created. Check the markdown file within the folder marked with their names for additional details.

6/22/2023 - Copyright/License Update

## License Notice

This work includes material taken from the System Reference Document 5.1 (“SRD 5.1”) by Wizards of the Coast LLC and available at https://dnd.wizards.com/resources/systems-reference-document. The SRD 5.1 is licensed under the Creative Commons Attribution 4.0 International License available at https://creativecommons.org/licenses/by/4.0/legalcode.

This work includes material written by Seth Hartman (aka ShadowsStride) and is licensed under the Creative Commons Attribution 4.0 International License available at https://creativecommons.org/licenses/by/4.0/legalcode.