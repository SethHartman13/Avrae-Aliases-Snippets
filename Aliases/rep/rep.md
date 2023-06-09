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
{"name": "Renown", "10":["+1 Spell Focus", "+1 Shield", "10x10 Plot of Land"], "15": ["+1 Armor"], "20": ["+2 Spell Focus","+2 Shield", "10x20 Plot of Land"], "25": ["+2 Armor"], "30": ["+3 Spell Focus", "+3 Shield", "20x20 Plot of Land"], "35": ["+3 Armor"], "imgurl": "www.someimage.png"}
```

For each "threshold," you need to have the key be a string and the value to be a list of strings. i.e. the threshold is 10 and the items you can get at reputation level 10 is Jelly Beans and Cotton Candy:

```"10": ["Jelly Beans", "Cotton Candy"]```

Here is template that you can use:
```json
{"name": "Name of org", "10":[""], "15": [""], "20": [""], "25": [""], "30": [""], "35": [""], "imgurl": ""}
```

### Organization List Server Variable
Thi server variable uses a json in order to work properly. You must use the svar name ***org_settings*** You can set the key values to be anything (as long there is no duplicates), but I recommend using numbers in ascending order (as strings). The values closer to the beginning of the json will be checked first. Here is an example:
```json
{"1": "Renown", "2": "uni_fed_settings", "3": "potato_uni_settings"}
```

For each organization name, you will need to have it match the name of the server variable you created up in [Organization Server Variable](#organization-server-variable). If you named the server variable for the Renowned as "RenRep" then you need to insert "RenRep" in the Organization List Server Variable.

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

## Source Code:

```py
embed
<drac2>

def main(inputs) -> list:

    # Grabs cvar and creates error list
    ch=character()
    error = []

    # Checks to see if it has the valid number of inputs
    if len(inputs) == 1 or len(inputs) == 2:

        # Lowercases input
        rep_input = inputs[0].lower()

        # Starts rewards list
        rewards = ["**Available redemption list:**"]

        # If checking rep/getting help
        if len(inputs) == 1:
            num = 0
        
        # If adding/subtracting from rep
        else:
            
            # Checks to see if second argument is an integer
            try:
                int(inputs[1])
            except "ValueError":
                rep_input = "Error"
                error.append("Integer expected in second argument")
            else:
                num = int(inputs[1])

    # If it does not have a valid number of inputs
    else:
        rep_input = "Error"
        error.append("Expected 1 or 2 arguments")

    # Grabs the organization dictionary
    organization_dictionary = load_json(get_svar("org_settings"))
    organization_list = []
    for value in organization_dictionary.values():
        organization_list.append(value)

    # If the svar is empty
    if len(organization_list) == 0 or organization_list == "0":
        rep_input = "Error"
        error.append("svar org_list does not exist!")

    # If the svar is not empty
    else:
        org_dictionaries = []
        try:
            for org in organization_list:
                org_dictionaries.append(load_json(get_svar(org)))
                

            org_names = []

            for org_dict in org_dictionaries:

                # Verifies that the dictionary has the name property
                try:
                    org_names.append(org_dict["name"])
                except:
                    error.append(f"Problem with dictionary {org_dict} with name")
        except:
            rep_input = "Error"
            error.append("svar org_list does not exist!")
            
    # If there have been no errors so far
    if len(error) == 0:

        # Creates boolean
        repfound = 0

        # For each organization, it will create iterations, then compare input against them
        for org_name in org_names:

            # Makes it so that the first organization found first is selected
            if repfound == 0:

                # Creates all the valid iterations
                initial_org_iterations = []
                org_iterations = []
                lst = []
                lst[:] = org_name.lower()


                for i in range(len(org_name) + 1):
                    initial_org_iterations.append(lst[:i])

                # So, what happens is it will create iterations like 'r' and 're'
                # This removes the first two so that at least three letters are needed
                initial_org_iterations.pop(0)
                initial_org_iterations.pop(0)

                # Puts the iterations into a single list.
                for iteration in initial_org_iterations:
                    org_iterations.append("".join(iteration))

                # If it does find an organization
                if rep_input in org_iterations:
                    rep_input = org_name
                    repfound = 1

                    # Pulls the dictionary and sets it as the dictionary to pull form
                    for dictionary in org_dictionaries:
                        if rep_input == dictionary["name"]:
                            global_dictionary = dictionary
                        else:
                            pass

                else:
                    pass

            else:
                pass
        
        # If it does not find an organization
        if repfound == 0:
            error.append("Organization not found")
            rep_input = "Error"

        else:
            pass

    else:
        pass

    
    if len(error) == 0:
        org_name = global_dictionary["name"]
        cc = f"Rep - {org_name}"
        desc = f"reputation with {org_name}"

        ch.create_cc_nx(cc, None, None, "none", "Number", None, None, cc, desc, 0)
        ch.mod_cc(cc, num)

        # Gets reputation amount
        currentcc = ch.get_cc(cc)

        # Finds keys that are supposed to be integers
        int_keys = []

        for key in global_dictionary.keys():

            try:
                int(key)
            except "ValueError":
                pass
            else:
                int_keys.append(key)

        thresholds = []

        # For each key that is below the current cc value
        for key in int_keys:

            if currentcc >= int(key):
                thresholds.append(key)

        # If there is at least 1 threshold breached, it will print out the rewards for that value
        if len(thresholds) > 0:
            for threshold in thresholds:
                rewards.append(f"**{threshold} Points:**")
                for item in global_dictionary[threshold]:
                    rewards.append(item)
                rewards.append("")

        else:
            rewards.append("None")

        # Join together all the rewards into a string
        rewardstring = "\n".join(rewards)
    
    else:
        pass

    # If there are no errors, then it writes out a title describing what the code did
    if len(error) == 0:
        if num >= 1:
            title = f"{name} adds {num} to their {desc}"
        elif num <= -1:
            title = f"{name} subtracts {abs(num)} from their {desc}"
        else:
            title = f"{name} checks their {desc}"

        try:
            thumbnail = global_dictionary["imgurl"]
        except:
            thumbnail = "https://raw.githubusercontent.com/SethHartman13/Avrae-Aliases-Snippets/master/Aliases/rep/image.png"

    # If there was an error, it writes out the errors
    else:
        title = f"{name} had following error(s) occur:"
        rewardstring = ", ".join(error)
        currentcc = "N/A"
        thumbnail = "https://raw.githubusercontent.com/SethHartman13/Avrae-Aliases-Snippets/master/Aliases/rep/image.png"

    # Handles outputs
    output_list = []
    output_list.append(title)
    output_list.append(rewardstring)
    output_list.append(f"**Current Rep: {currentcc}**")
    output_list.append(thumbnail)

    return output_list

# Main function
output = main(&ARGS&)

title = output[0]
rewardstring = output[1]
currentcc = output[2]
thumbnail = output[3]
left_carrot = "<"

</drac2>

-title "{{title}}"
-f "{{rewardstring}}"
-f "{{currentcc}}"
-thumb "{{thumbnail}}"
-footer "!rep [organization] {{left_carrot}}#> | Updated 6/8/23 | ShadowsStride"
```

## Copyright Notice

Copyright 2023 Seth Hartman (aka ShadowsStride)

All rights reserved.

The code and images I own in this repository are protected by copyright law. Unauthorized use, reproduction, or distribution of this material is strictly prohibited. This includes, but is not limited to, copying large portions of code or uploading the code and images to any other platform or website without written consent.

If you wish to use or reproduce any part of this repository, please contact ShadowsStride at shadowsstride@gmail.com for permission.

Any infringement of copyright will result in legal action.