1. The data base - info on deployment, dev info, etc.
## Resources

### User

The user is polymorphic depending on the role of the user. Dieticians will be linked to clients either through a join table DieticianClients, or through a double join, DieticianOrganization and OrganizationClients. 

- id : int
- role : var_char (client, dietician, clinic_admin, site_admin)
- pw_hash : char
- first_name : var_char
- last_name : var_char
- email : var_char
- phone : var_char
- address : var_char


### Key

### Food

### Meal

## Dietary Data

A key component in making KetoPal a success, and serving families with a high quality, reliable and safe meal plans is the quality of the data for 'food items' (We are borrowing the FDC terminology of food item, in KDC they are just called 'foods', and synonyms we could have reasonably chosen include ingredient, or component). The patient who is on the medical keto diet is relying on the information being correct for their health, so we want to pull from trusted and verified sources. Thus, we have chosen the [FoodData Central](https://fdc.nal.usda.gov/index.html) api/data to populate our initial data set. They have pulled together 5 different data sets, all from goverment agencies and labs, and made them available through a single api. I won't redocument their api here, as their documentation is good and complete. I've created python scripts in the `tools/foodItems` directory for paging through their data set, massaging the data into a more application friendly format, and for Posting the food items to the database. 

Dieticians will still need to add food items for their clients that aren't in the FDC data set, and we may at a future time decide to canonize the additions the dieticians make into a supplemental dataset. 
