1. The data base - info on deployment, dev info, etc.
## Resources

### User

The user is polymorphic depending on the role of the user. Dieticians will be linked to clients either through a join table DieticianClients, or through a double join, OrganizationDieticians and OrganizationClients. 

- id : int NotNull
- role : var_char (client, dietician, organization_admin, site_admin) NotNull
- pw_hash : var_char NotNull
- email : var_char NotNull
- first_name : var_char
- last_name : var_char
- phone : var_char
- address_line_1 : var_char
- address_line_2 : var_char
- city : var_char
- state : char(2) 
- zip : var_char
- created : timestamp NotNull
- updated : timestamp NotNull

### Organization

An organization represents a group of dieticians/physicians who collectively manage a group of clients. Each organization must have at least one organization_admin, and must have exactly one primary_organization_admin. The primary will have special privalages, and would be who we contact when needed.

- id : int NotNull
- name : var_char
- phone : var_char
- primary_organization_admin : int FK NotNull 
- address_line_1 : var_char
- address_line_2 : var_char
- city : var_char
- state : char(2) 
- zip : var_char
- created : timestamp NotNull
- updated : timestamp NotNull


### OrganizationDieticians

A simple join table linking an organization to their group of dieticians. (M:M)


### OrganizationClients

A simple join table linking an organization to their group of clients. (M:M)


### DieticianClients

A simple join table linking a dietician to their group of clients. (M:M)



### Key

The key is the core way the app securely accesses the api. 

- id : char NotNull
- user_id : int FK NotNull
- expires : timestamp NotNull
- created : timestamp NotNull
- updated : timestamp NotNull


### Food

Food items are the basic building blocks for recipes and are imported from the dietary data sources below, or created by a clients dietician. 

- id : var_char NotNull
- name : var_char 
- dietician_id : var_char FK
- carbs : float
- fats : float
- protien : float
- micros : var_char

### Recipe

Recipes are the base unit for building meals/snacks. They are polymorphic based on role and contain the metadata; title, date, etc.

- id : char NotNull
- user_id : int FK NotNull
- role : char (snack, meal)
- title : var_char
- notes : var_char
- created: timestamp NotNull
- updated : timestamp NotNull


## Dietary Data

A key component in making KetoPal a success, and serving families with a high quality, reliable and safe meal plans is the quality of the data for 'food items' (We are borrowing the FDC terminology of food item, in KDC they are just called 'foods', and synonyms we could have reasonably chosen include ingredient, or component). The patient who is on the medical keto diet is relying on the information being correct for their health, so we want to pull from trusted and verified sources. Thus, we have chosen the [FoodData Central](https://fdc.nal.usda.gov/index.html) api/data to populate our initial data set. They have pulled together 5 different data sets, all from goverment agencies and labs, and made them available through a single api. I won't redocument their api here, as their documentation is good and complete. I've created python scripts in the `tools/foodItems` directory for paging through their data set, massaging the data into a more application friendly format, and for Posting the food items to the database. 

Dieticians will still need to add food items for their clients that aren't in the FDC data set, and we may at a future time decide to canonize the additions the dieticians make into a supplemental dataset. 
