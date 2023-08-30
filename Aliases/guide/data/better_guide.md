# User Guide

Welcome to the user guide used to create guides of your own (and guides that shared through gvars).

## JSON Structure

The guide alias's data is organized into different guides within `guide_dict`, each containing specific sections. Here's how the information is structured:

```json
{
    "Guide 1": {
        "Section 1": "Some singular paragraph",
        "Section 2": {
            "Header": "Header paragraph of heading 2", // This header paragraph has to have key be "Header"
            "Sub-section 1": "Contents of sub-section 1",
            "Sub-section 2": "Contents of sub-section 2",
            "Sub-section 3": "Contents of sub-section 3"
        }
    },
    "Guide 2": {
        "gvar": "gvar GUID string" // Would have content structured like Guide 1
    },
    "Guide 3": {
        "svar": "name of svar" // Would have content structured like Guide 1
    },
    "Guide 4": {
        "uvar": "name of uvar" // Would have content structured like Guide 1
    }
}
```

### Guide 1

Under "Guide 1," you'll find two sections: "Section 1" and "Section 2."

#### Section 1

This section contains a singular paragraph that provides enough information to the topic that sub-sections are not necessary

#### Section 2

In "Section 2," you'll find more detailed content structured with multiple levels that require sub-sections.

- **Header**: This is the introductory paragraph for "Heading 2." It sets the stage for the subsequent sub-sections.
- **Sub-section 1**: Here, you'll find the contents related to sub-section 1.
- **Sub-section 2**: Here, you'll find the contents related to sub-section 2.
- **Sub-section 3**: Here, you'll find the contents related to sub-section 3.

### Guide 2

"Guide 2" introduces a different type of content structure. It includes a GUID string of a gvar (global variable). The content under "Guide 2" follows a similar pattern to "Guide 1," but with different content.

### Guide 3

"Guide 3" presents yet another variation. It includes the name of a svar (server variable). Like the previous titles, the content here is structured similarly to "Guide 1."

### Guide 4

"Guide 4" presents one last variation. It includes the name of a uvar (user variable). Like the previous titles, the content here is structured similarly to "Guide 1."

## Accessing Guide Sections

To help you access information, you can query the guides located on your server at several levels. **Note:** Due to character limitations within Discord, you may need to provide a list number. Simply add that to the end of your query Ex. `!guide "Guide 1" 3`. Server staff can help avoid this by reducing the length of sections, and sub-sections. Server members can also be more specific in their queries (adding section and sub-section):

### General
Running `!guide` will bring up the guides and sections on your server. Using the json above, it would display the following (**s and #s will not show as it follows markdown formatting rules):
```md
## Guides

**Guide 1**
Section 1
Section 2

**Guide 2**

**Guide 3**

**Guide 4**
```

### Guide
Running `!guide [guide name]` will bring up the sections and the sub-sections within those sections. Using the json above, `!guide "Guide 1"` will display the following (**s and #s will not show as it follows markdown formatting rules)
```md
## Section 1
Some singular paragraph or something

## Section 2
Header paragraph of Section 2

**Sub-section 1**

**Sub-section 2**

**Sub-section 3**
```

If you enter in a guide name that does not exist, the program will display an output similar to [General](#general).

### Section
Running `!guide [guide name] [section name]` will bring up the section and the content within the section. Using the json above `!guide "Guide 1" "Heading 2"` will display the following (**s and #s will not show as it follows markdown formatting rules):
```md
## Section 2
Header paragraph of Section 2

**Sub-section 1**
Contents of Sub-section 1

**Sub-section 2**
Contents of Sub-section 2

**Sub-section 3**
Contents of Sub-section 3
``` 

If you enter in a section name that does not exist, the program will display an output similar to [Guide](#guide)

### Sub-section
Running `!guide [guide name] [section name] [sub-section name]` will bring up the contents within a sub-section. Using the json above `!guide "Guide 1" "Heading 2" "Sub-section 1` will display the following (**s will not show as it follows markdown formatting rules):
```md
**Sub-section 1**
Contents of Sub-section 1
```

If you enter in a sub-section name that does not exist, the program will display an output similar to [Section](#section)