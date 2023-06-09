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
    - Fog/Mist
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

You will need to run `!svar weather_location_list` to copt over the previous settings before you update the server variable as it overwrites the existing data.

## Changelog:
6/8/2023 - Alias created and documentation written.

6/8/2023 - Subalias [help](https://github.com/SethHartman13/Avrae-Aliases-Snippets/blob/master/Aliases/weather/help/help.md) has been created. Check the markdown files within the folders marked with their names for additional details

## Source Code:
```py
embed
<drac2>

def roll_dice(dice_type:str, baseline: int = 0) -> list:
    """
    Rolls dice and puts together string to use.

    Args:
        dice_type (str): What dice to roll
        baseline (int): What to add to the dice roll

    Return:
        (list): List of results

    """
    
    # Rolls dice
    roll_obj = vroll(dice_type)

    # If baseline is 0
    if baseline == 0:
        roll_string = f"{roll_obj.dice} = {roll_obj.total}"
    
    # If baseline is not 0
    else:
        roll_string = f"{roll_obj.dice} + {baseline} = {baseline + roll_obj.total}"

    return [roll_string, baseline + roll_obj.total]


def to_celsius(degrees: int) -> float:
    """
    Converts Fahrenheit to Celsius

    Args:
        degrees (int): Temperature to be converted

    Return:
        (float): Results of the conversion

    """
    return round((degrees - 32) * (5/9), 1)


def main(args: list) -> list:
    """
    Main alias function

    Args:
        args: List of arguments provided

    Return:
        (list): Outputs for the embed card

    """

    # Sets up error list and sets valid weather conditions
    error = []
    seasons = ['Fall', 'Spring', 'Summer', 'Winter', 'Autumn']
    weather_water_conditions = ["fog/mist", "light", "heavy", "overcast", "clear"]
    weather_wind_conditions = ["light wind", "heavy wind", "gentle breeze", "none"]
    
    # If there is at least 1 argument
    if len(args) > 0:
        try:
            # Grab the settings dict
            weather_settings_dict = load_json(get_svar("weather_location_list"))
            location_list = []

            # Puts all the names of the svars used for location settings
            for value in weather_settings_dict.values():
                    location_list.append(value)

            # Grabs the dictionaries for each of the locations and puts them in a list
            location_dictionaries = []
            for location in location_list:
                location_dictionaries.append(load_json(get_svar(location)))

        except:
            error.append("Problems loading dictionaries")

        # If it did not have any problems loading dictionaries           
        if len(error) == 0:

            # Figure out what the first argument was
            season_input = args[0].lower()

            # For each season, it will create iterations, then compare input against them
            seasonfound = 0
            for season_name in seasons:

                # Makes it so that the first season found first is selected
                if seasonfound == 0:

                    # Creates all the valid iterations
                    initial_season_iterations = []
                    season_iterations = []
                    lst = []
                    lst[:] = season_name.lower()


                    for i in range(len(season_name) + 1):
                        initial_season_iterations.append(lst[:i])

                    # So, what happens is it will create iterations like 'f' and 'fa'
                    # This removes the first two so that at least three letters are needed
                    initial_season_iterations.pop(0)
                    initial_season_iterations.pop(0)

                    # Puts the iterations into a single list.
                    for iteration in initial_season_iterations:
                        season_iterations.append("".join(iteration))

                    # If it does find an season
                    if season_input in season_iterations:
                        season_input = season_name
                        seasonfound = 1

                        # Allows it so that Autumn is a valid season, but will map it to Fall
                        if season_input.lower() == "autumn":
                            season_input = "Fall"
                        else:
                            pass

                    else:
                        pass

                else:
                    pass

            # If it does not find an organization
            if seasonfound == 0:
                error.append("Season not found.")

            else:
                pass

        else:
            pass

        # If it doesn't have any errors
        if len(error) == 0:

            # Creates results list
            results = []

            # For each location setting dictionary found
            for location_dictionary in location_dictionaries:

                try:
                    # Grab name of location
                    results.append(f"**{location_dictionary['name']}:**")

                    # Grab season settings for the season requested
                    season_settings = location_dictionary[season_input]

                    # Roll each of the different weather conditions
                    temperature_roll_list = roll_dice(season_settings['temp_dice'], season_settings['temp_base'])
                    water_roll_list = roll_dice(season_settings['water_chance_dice'])
                    wind_roll_list = roll_dice(season_settings['wind_chance_dice'])
                
                except:
                    error.append("Problems rolling conditions")

#---------------------------------------------------------------------------------------------------------------------------------------
# Temperature rolls

                # If it doesn't have any errors
                if len(error) == 0:

                    try:
                        # Checks to see if it is freezing
                        if temperature_roll_list[1] <= 32:
                            freezing = 1
                        else:
                            freezing = 0

                        # Adds the temperature results to the results list
                        results.append(f"{temperature_roll_list[0]} degrees fahrenheit ({to_celsius(temperature_roll_list[1])} degrees celsius)")
                        results.append("")
                    except:
                        error.append(f"There was an error rolling temperature for {location_dictionary['name']}")

#---------------------------------------------------------------------------------------------------------------------------------------
# Water rolls

                    # If it doesn't have any errors
                    if len(error) == 0:

                        try:
                            # Iterates through the water thresholds
                            for key in season_settings['water_roll_thresholds'].keys():
                                if water_roll_list[1] >= int(key):
                                    water_result = season_settings['water_roll_thresholds'][key]
                                else:
                                    pass

                            # Checks to see if it has a valid water condition
                            if water_result.lower() in weather_water_conditions:
                                
                                # Heavy moisture, sets moisture rate, adds disadvantage note
                                if water_result.lower() == "heavy":
                                    water_rate = randint(5,20) / 10
                                    disadv = "Disadvantage on Wisdom (Perception) checks"
                                    
                                # Fog/Mist, adds disasvantage note
                                elif water_result.lower() == "fog/mist":
                                    water_rate = 0
                                    disadv = "Disadvantage on sight-based Wisdom (Perception) checks"

                                # Light Moisture, sets moisture rate
                                elif water_result.lower() == "light":
                                    water_rate = randint(1,3) / 10
                                    disadv = "None"

                                # Conditions that don't have any amount of moisture or disadvantage
                                else:
                                    water_rate = 0
                                    disadv = "None"

                                # For heavy and light moisture, says if it is rain or snow based upon temperature and formats data (also converts in/hr to mm/hr)
                                if water_result.lower() == "light" or water_result.lower() == "heavy":
                                    if freezing == 0:
                                        water_result = f"`{water_result} Rain`  {water_rate} in/hr ({round(water_rate * 25.4,1)} mm/hr)"
                                    else:
                                        water_result = f"`{water_result} Snow`  {water_rate} in/hr ({round(water_rate * 25.4,1)} mm/hr)"

                                # Formats data if it is not heavy or light moisture
                                else:
                                    water_result = f"`{water_result}`"                                

                                # Adds results to the results list
                                results.append(f"{water_roll_list[0]} {water_result}")

                                # Adds disadvantage note to results list
                                if disadv != "None":
                                    results.append(f"**{disadv}**")
                                    results.append("")

                                # Adds space to results list
                                else:
                                    results.append("")

                            # If there was an invalid moisture type
                            else:
                                error.append(f"Invalid moisture type for {location_dictionary['name']}")


                        except:
                            error.append(f"There was an error rolling moisture for {location_dictionary['name']}")

#---------------------------------------------------------------------------------------------------------------------------------------
# Wind rolls
                        # If it doesn't have any errors
                        if len(error) == 0:

                            try:
                                # Iterates through the wind thresholds
                                for key in season_settings['wind_roll_thresholds'].keys():
                                    if wind_roll_list[1] >= int(key):
                                        wind_result = season_settings['wind_roll_thresholds'][key]
                                    else:
                                        pass

                                # Checks to see if it has a valid wind condition
                                if wind_result.lower() in weather_wind_conditions:

                                    # Heavy wind, sets wind speed, adds disadvantage note (also converts from mph to km/h)
                                    if wind_result.lower() == "heavy wind":
                                        wind_rate = randint(25,54)
                                        wind_result = f"`{wind_result}`  {wind_rate} mph ({round(wind_rate * 1.60934, 1)} km/h)"
                                        disadv = "Disadvantage on ranged weapon attacks"

                                    # Light wind, sets wind speed (also converts from mph to km/h)
                                    elif wind_result.lower() == "light wind":
                                        wind_rate = randint(8,54)
                                        wind_result = f"`{wind_result}`  {wind_rate} mph ({round(wind_rate * 1.60934, 1)} km/h)"
                                        disadv = "None"

                                    # Gentle breeze, sets wind speed (also converts from mph to km/h)
                                    elif wind_result.lower() == "gentle breeze":
                                        wind_rate = randint(1,7)
                                        wind_result = f"`{wind_result}`  {wind_rate} mph ({round(wind_rate * 1.60934, 1)} km/h)"
                                        disadv = "None"

                                    # No wind
                                    else:
                                        wind_result = f"`{wind_result}`"
                                        disadv = "None"

                                    # Adds results to results list
                                    results.append(f"{wind_roll_list[0]} {wind_result}")

                                    # Adds disadvantage note to results list
                                    if disadv != "None":
                                        results.append(f"**{disadv}**")
                                        results.append("")

                                    # Adds space to results list
                                    else:
                                        results.append("")

                                # If there was an invalid wind type
                                else:
                                    error.append(f"Invalid wind type for {location_dictionary['name']}")


                            except:
                                error.append(f"There was an error rolling wind for {location_dictionary['name']}")

                        else:
                            pass
                    else:
                        pass
                else:
                    pass

                # Adds space to exit
                if len(error) == 0:
                    results.append("")
                else:
                    pass
        else:
            pass

    # If no arguments were passed
    else:
        error.append("You are missing the season argument")

    # If there were no errors, creates title and it joins all the results into a single string
    if len(error) == 0:
        title = "Daily weather report"
        result_string = "\n".join(results)

    # If there were errors, creates title and it joins all the errors into a single string
    else:
        title = "Error running daily weather report"
        error_string = '\n'.join(error)
        result_string = f"Error(s):\n{error_string}"

    # Returns results
    return [title, result_string]

# Calling main function
output = main(&ARGS&)

# Prepares outputs for embed insert
title = output[0]
result_string = output[1]

</drac2>

-title "{{title}}"
-f "{{result_string}}"
-thumb "https://raw.githubusercontent.com/SethHartman13/Avrae-Aliases-Snippets/master/Aliases/weather/image.png"
-footer "!weath [season] | Updated 6/8/2023 | ShadowsStride"
```


## Copyright Notice

Copyright 2023 Seth Hartman (aka ShadowsStride)

All rights reserved.

The code and images I own in this repository are protected by copyright law. Unauthorized use, reproduction, or distribution of this material is strictly prohibited. This includes, but is not limited to, copying large portions of code or uploading the code and images to any other platform or website without written consent.

If you wish to use or reproduce any part of this repository, please contact ShadowsStride at shadowsstride@gmail.com for permission.

Any infringement of copyright will result in legal action.