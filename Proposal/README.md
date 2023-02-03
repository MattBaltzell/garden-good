### Capstone 2 Project Proposal

# **Garden Good App**

In an attempt to provide their wallets some relief from the rising grocery prices, many people have created small vegetable garden's in their yards. Unfortunately, these gardeners do not have adequate knowledge to optimize their harvest. So, they miss out on a lot of great veg. If only there was a tool they could use to maximize their garden's output...

## Project Goals

The Garden Good app helps beginning gardeners and experienced gardeners plan, plant, and tend their crops for an abudant harvest. This app incorporates planting zones and proper timing for sowing, growth and tending information, as well as weather alerts to help your garden thrive. From proper feeding and watering to pruning and pests, this app will help you garden GOOD. 

---

## User Demographics

Garden Good is targeted towards hobbyist and urban gardeners that want a way to quickly reference information in order to maintain healthy plants and a flourishing garden.

---

## Data and API Usage

### **Garden Good API**

This app will be powered by the Garden Good API which I will build. This API will include data for plants, including but not limited to the following: name, hardiness, spacing, amount of sun, amount of water, fertilizing instructions ,time until maturation, ideal plant pairings, pruning/trimming reminders. The API will also handle the creation and updating of users' gardens and beds, as well as provide Auth routes for the user.

### **Plant Hardiness Zone API**

https://rapidapi.com/fireside-worldwide-fireside-worldwide-default/api/plant-hardiness-zone

This app will use the **Plant Hardiness Zone API** in order to determine the hardiness zone in which the user resides. The app will then use this information to provide the user with the correct planting and care instructions for their hardiness zone.

### **WeatherAPI**

https://www.weatherapi.com/

This app will make use of the **WeatherAPI** in order to help the user properly care for their plants during various weather conditions such as extreme heat, freezes, and precipitation.

---

## Project Approach

My approach for creating the Garden Good App will be to develop an MVP focused on the geolocation features first, and then adding the messaging features as the app evolves.

### **Database Schema**

Database models will consist of the following:

- User
- Garden
- Bed
- Plant

Relationships: 

- The User model will have a many-to-many relationship with the Garden model, so that users in the same household can share gardens, and Users can manage multiple Gardens across multiple properties.
- The Garden model will have a one-to-many relationship with the Bed model, so a garden can have multiple beds throughout the property.
- The Bed model will have a many-to-many relationship with the Plant model, so multiple Beds can contain the same type of Plants, and multiple Plants can be found in each Bed.

![database schema]() - Coming Soon

### **Potential Issues**

1. In the event that the Plant Hardiness Zone API goes down, a new user should be able to manually choose a hardiness zone.  
   When a hardiness zone is set manually, there should be a state such as "hasManualHardinessZone" that will trigger the Hardiness Zone API to reset the user's hardiness zone during the next login.  
   Since the registration process will require the user's zip code, the API will be able to properly set the user's hardiness zone and set "hasManualHardinessZone" to false.
2. If the WeatherAPI is down, the user will not receive weather-related care alerts until the API is running again.

### **Security & Sensitive Information**

- User email addresses and zip codes will be stored for registering a new user.
- Password security will be handled with Bcrypt.
- The app does not currently have a payment feature, but may be added in the future.

### **Functionality**

-

### **User Flows**

User.....
![user flow diagram]() - Coming Soon

### **Stretch Goals**

1. Add common garden pest and pest control data
2. Add common preserving techniques for each veggie
3. Add bed building techniques to help new gardeners get started (tips like leave room to walk and dont make the bed bigger than you can reach) maybe this can have a user add feature where people can suggest ideas and share experiences
4. Building plans for different types of beds
