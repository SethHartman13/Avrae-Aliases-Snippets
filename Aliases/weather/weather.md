<h1>Weather Alias<img align="right" src="image.png" width="100px"></h1>
Weather alias that handles weather with regions and locations.

## Owner(s):
- Me (ShadowsStride)

## Current Plans:
- None

## Help:
`!weath [season]`

In order to run this properly, you need to do the following:
- Create a server variable for each location/region (i.e. Falkland Islands)
- Create a server variable containing the name of the svars for each organization called `weather_location_list`

### Location Server Variable
This server variable uses a json in order to work properly. It uses the "name" property to identify the name of the location. Then it organizes the weather settings by season: Here is an example
```json
{
    "name": "Haell",
    "Winter": { "temp_dice": "2d6", "temp_base": 60, "water_chance_dice": "1d20", "water_roll_thresholds": {"1":"Clear", "3": "Overcast", "5": "Fog/Mist", "8": "Light", "17": "Heavy"}, "wind_chance_dice": "1d20", "wind_roll_thresholds": {"1": "None", "4": "Gentle Breeze", "10": "Light Wind", "16": "Heavy Wind"}
    },

    "Spring": { "temp_dice": "2d6", "temp_base": 60, "water_chance_dice": "1d20", "water_roll_thresholds": {"1":"Clear", "3": "Overcast", "5": "Fog/Mist", "8": "Light", "17": "Heavy"}, "wind_chance_dice": "1d20", "wind_roll_thresholds": {"1": "None", "4": "Gentle Breeze", "10": "Light Wind", "16": "Heavy Wind"}
    },

    "Summer": { "temp_dice": "2d6", "temp_base": 60, "water_chance_dice": "1d20", "water_roll_thresholds": {"1":"Clear", "3": "Overcast", "5": "Fog/Mist", "8": "Light", "17": "Heavy"}, "wind_chance_dice": "1d20", "wind_roll_thresholds": {"1": "None", "4": "Gentle Breeze", "10": "Light Wind", "16": "Heavy Wind"}
    },

    "Fall": { "temp_dice": "2d6", "temp_base": 60, "water_chance_dice": "1d20", "water_roll_thresholds": {"1":"Clear", "3": "Overcast", "5": "Fog/Mist", "8": "Light", "17": "Heavy"}, "wind_chance_dice": "1d20", "wind_roll_thresholds": {"1": "None", "4": "Gentle Breeze", "10": "Light Wind", "16": "Heavy Wind"}
    }
}
```
For each season it uses the following properties:
- temp_dice (str): Dice used to add to base temperature
- temp_base (int): Base temperature
- water_chance_die (str): Dice used to roll what moisture will be dropped (if any)
- water_roll_thresholds(dict(str:str)): Thresholds that result in the moisture received. Here are the valid moisture conditions (heavy and light adapt to current temperature on wether it is rain or snow):
    - Clear
    - Overcast
    - Mist
    - Heavy Fog
    - Light
    - Heavy
- wind_chance_dice (str): Dice used to roll what wind will occur (if any)
- wind_roll_thresholds(dict(str:str)): Thresholds that result in the wind conditions. Here are the valid wind conditions:
    - None
    - Gentle Breeze
    - Light Wind
    - Heavy Wind

**Note: Both water and wind thresholds must have a value at 1**

Here is a template that you can use:
```json
{
    "name": "location",
    "Winter": { "temp_dice": "", "temp_base": 60, "water_chance_dice": "1d20", "water_roll_thresholds": {"1":"Clear", "10": "", "15": "", "20": ""}, "wind_chance_dice": "1d20", "wind_roll_thresholds": {"1": "None", "5": "", "10": "", "15": ""}
},

    "Spring": { "temp_dice": "", "temp_base": 60, "water_chance_dice": "1d20", "water_roll_thresholds": {"1":"Clear", "10": "", "15": "", "20": ""}, "wind_chance_dice": "1d20", "wind_roll_thresholds": {"1": "None", "5": "", "10": "", "15": ""}
},

    "Summer": { "temp_dice": "", "temp_base": 60, "water_chance_dice": "1d20", "water_roll_thresholds": {"1":"Clear", "10": "", "15": "", "20": ""}, "wind_chance_dice": "1d20", "wind_roll_thresholds": {"1": "None", "5": "", "10": "", "15": ""}
},

    "Fall": { "temp_dice": "", "temp_base": 60, "water_chance_dice": "1d20", "water_roll_thresholds": {"1":"Clear", "10": "", "15": "", "20": ""}, "wind_chance_dice": "1d20", "wind_roll_thresholds": {"1": "None", "5": "", "10": "", "15": ""}
    }
}
```

### Weather Location List Server Variable
This server variable uses a json in order to work properly. You must use the scar name ***weather_location_list*** You can set the key values to be anything (as long as there are no duplicates), but I recommend using numbers in ascending order (as strings). The values closer to the beginning of the json will be run first. Here is an example:
```json
{"1": "haell_weather_settings", "2": "falkland_weather_settings", "3": "mythran_weather_settings"}
```

For each location name, you will need to have it match the name of the server variable you created in [Location Server Variable](#location-server-variable). If you named the server varable for Haell as "haellWeather" then you will need to insert "haellWeather" in the Weather Location List server variable.

Here is a template that you can use:
```json
{"1": "Location 1 svar", "2": "Location 2 svar", "3": "Location 3 svar"}
```

**UPDATING THIS SERVER VARIABLE**

You will need to run `!svar weather_location_list` to copy over the previous settings before you update the server variable as it overwrites the existing data.

## Changelog:
6/8/2023 - Alias created and documentation written.

6/8/2023 - Subalias [help](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/weather/help/help.md) has been created. Check the markdown files within the folders marked with their names for additional details

6/14/2023 - Copyright notice updated

6/23/2023 - Copyright/License Update and changing of valid water weather types

6/27/2023 - Optimization of dictionary searching code. UI update. Removal of wind/water weather validation, any weather types that do not fit the ones listed in [Location Server Variable](#location-server-variable).

## License Notice

This work includes material taken from the System Reference Document 5.1 (“SRD 5.1”) by Wizards of the Coast LLC and available at https://dnd.wizards.com/resources/systems-reference-document. The SRD 5.1 is licensed under the Creative Commons Attribution 4.0 International License available at https://creativecommons.org/licenses/by/4.0/legalcode.

This work includes material written by Seth Hartman (aka ShadowsStride) and is licensed under the Creative Commons Attribution 4.0 International License available at https://creativecommons.org/licenses/by/4.0/legalcode.