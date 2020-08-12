1. The data base - info on deployment, dev info, etc.
2. The resources

## Dietary Data

A key component in making KetoPal a success, and serving families with a high quality, reliable and safe meal plans is the quality of the data for 'food items' (We are borrowing the FDC terminology of food item, in KDC they are just called 'foods', and synonyms we could have reasonably chosen include ingredient, or component). The patient who is on the medical keto diet is relying on the information being correct for their health, so we want to pull from trusted and verified sources. Thus, we have chosen the [FoodData Central](https://fdc.nal.usda.gov/index.html) api/data to populate our initial data set. They have pulled together 5 different data sets, all from goverment agencies and labs, and made them available through a single api. I won't redocument their api here, as their documentation is good and complete. I've created python scripts in the `tools/foodItems` directory for paging through their data set, massaging the data into a more application friendly format, and for Posting the food items to the database. 

Dieticians will still need to add food items for their clients that aren't in the FDC data set, and we may at a future time decide to canonize the additions the dieticians make into a supplemental dataset. 
