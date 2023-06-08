<h1>List Subalias<img align="right" src="../image.png" width="100px"></h1>

Subalias that lists out all known organizations.

## Owner(s):
- Me (ShadowsStride)

## Current Plans:
- None

## Help:
`!rep list` 

## Changelog:
6/6/2023 - Subalias created

6/8/2023 - Copyright notice and image added

## Source Code:

```py
embed
<drac2>
# Grabs cvar and creates error list

def main() -> list:

    ch=character()

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
                    org_names.append(f"**{org_dict['name']}**")
                except:
                    error.append(f"Problem with dictionary {org_dict} with name")
        except:
            rep_input = "Error"
            error.append("svar org_list does not exist!")
            
        title = f"{name} checks all known organizations"
        orgstring = "/n".join(org_names)


    # Handles outsputs
    output_list = []
    output_list.append(title)
    output_list.append(orgstring)

    return output_list

# Main function
output = main()

title = output[0]
orgstring = output[1]

</drac2>

-title "{{title}}"
-f "{{orgstring}}"
-thumb "https://raw.githubusercontent.com/SethHartman13/Avrae-Aliases-Snippets/master/Aliases/rep/image.png"
-footer "!rep list | Updated 6/8/23 | ShadowsStride"
```

## Copyright Notice

Copyright 2023 Seth Hartman (aka ShadowsStride)

All rights reserved.

The code and images I own in this repository are protected by copyright law. Unauthorized use, reproduction, or distribution of this material is strictly prohibited. This includes, but is not limited to, copying large portions of code or uploading the code and images to any other platform or website without written consent.

If you wish to use or reproduce any part of this repository, please contact ShadowsStride at shadowsstride@gmail.com for permission.

Any infringement of copyright will result in legal action.