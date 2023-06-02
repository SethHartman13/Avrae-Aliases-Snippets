# Rep Alias

Reputation alias that handles reputation with organizations and groups. **Currently only supports organizations manually entered into the code**

## Owner(s):
- Me (ShadowsStride)

## Current Plans:
- The ability to add, modify, or remove organizations using a server variables.

## Code:

```py
embed
<drac2>

# Character variable
ch=character()

# Collects inputs
inputs = &ARGS&

# If it has the valid number of inputs
if len(inputs) == 1 or len(inputs) == 2:

    # Lowercases input and creates error variable
    rep_input = inputs[0].lower()
    error = "None"

    # Initial list starts
    rewards = ["Available redemption list:\n"]
    item_rewards = ["**Items:**"]
    land_rewards = ["**Land plots:**"]

# If it does not have the valid number of inputs
else:
    error = "Expected 1 or 2 arguments"
    rep_input = "Error"

# Valid Renown inputs
valid_renown = ['re', 'ren', 'reno', 'renow', 'renown']

# Valid Piety inputs
# valid_piety = ['pi', 'pie', 'piet', 'piety'] 

# Sets global valid inputs
valid_rep = []

for item in valid_renown:
    valid_rep.append(item)

# for item in valid_piety:
    # valid_rep.append(item)

# If there are no errors
if error == "None":

    # If one argument was given
    if len(inputs) == 1:
        num = 0

    # If two arguments were given
    else:

        # Checks to see if the second argument is a number
        try:
            num = int(inputs[1])
        except "ValueError":
            error = "Number not found in argument 2"

# If there is an error
else:
    pass

# If there was not an error raised before
if error == "None":

    # Renowned Reputation
    if rep_input in valid_renown:
        cc = "Rep - Renown"
        desc = "Reputation with the Renown"
        ch.create_cc_nx(cc, None, None, "none", "Number", None, None, cc, desc, 0)
        ch.mod_cc(cc, num)

        # Gets reputation amount
        currentcc = ch.get_cc(cc)

        # If greater than or equal to 10
        if currentcc >= 10:
            item_rewards.append("+1 Spell Focus (10 points)")
            item_rewards.append("+1 Shield (10 points)")
            land_rewards.append("10x10 Plot of Land (10 points)")
        

            # If greater than or equal to 15
            if currentcc >= 15:
                item_rewards.append("+1 Armor (15 points)")

                # If greater than or equal to 20
                if currentcc >= 20:
                    item_rewards.append("+2 Spell Focus (20 points)")
                    item_rewards.append("+2 Shield (20 points)")
                    land_rewards.append("10x20 Plot of Land (20 points)")

                    # If greater than or equal to 25
                    if currentcc >= 25:
                        item_rewards.append("+2 Armor (25 points)")

                        # If greater than or equal to 30
                        if currentcc >= 30:
                            item_rewards.append("+3 Spell Focus (30 points)")
                            item_rewards.append("+3 Shield (30 points)")
                            land_rewards.append("20x20 Plot of Land (30 points)")

                            # If greater than or equal to 35
                            if currentcc >= 35:
                                item_rewards.append("+3 Armor (35 points)")

    # Invalid input for organization
    else:
        error = "Unknown Reputation Entered"

# If there was an error
else:
    pass

# Error
if error != "None":
    rewardstring = "Choose from Renown"
    currentcc = "The format is `!rep organization #` to add, `!rep organization` to check"
    title = f"{name} made an error: {error}"

# No error
else:
    # Checks length of item rewards, adds to reward string if not 0
    if len(item_rewards) > 1:
        item_rewardstring = "\n".join(item_rewards)
        rewards.append(item_rewardstring)

    # Checks length of land rewards, adds to reward string if not 0
    if len(land_rewards) > 1:
        land_rewardstring = "\n".join(land_rewards)
        rewards.append(land_rewardstring)

    # If no rewards
    if len(rewards) == 1:
        rewards.append("None")

    # Rewards is converted into a string
    rewardstring = "\n".join(rewards)

    # Sets title based upon adding, subtracting, or checking
    if num >= 1:
        title = f"{name} adds {num} to their {desc}"
    elif num <= -1:
        title = f"{name} subtracts {abs(num)} from their {desc}"
    else:
        title = f"{name} checks their {desc}"

</drac2>

-title "{{title}}"
-f "{{rewardstring}}"
-f "Current Rep: {{currentcc}}"
-footer "!rep [organization] [#] | Updated 6/1/23 | ShadowsStride"
```