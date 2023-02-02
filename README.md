### Capstone 2 Project Proposal

# **Veggie Garden App**

In past years, musicians were able to visit their local guitar shops or music stores to socialize with other musicians, post ads on the bulletin boards, and find collaborations by being in the local music scene. While this method still works for some musicians, the popularity of music genres can differ greatly from city to city, making it difficult for many musicians to find their fit.

## Project Goals

The Veggie Garden app allows users to find data on the fruit and veggie plants in their garden. It helps them to plan their garden by ensuring plants are placed in the correct area of their garden and during the proper time of the year for their area. It also allows them to maintain healthy plants with information on proper feeding, watering, pruning, and pest control.

---

## User Demographics

The Veggie Garden app is targeted towards hobbyist gardeners that want a way to easily find information on the plants in their garden.

---

## Data and API Usage

### **Veggie Plant API**

This app will be powered by a Veggie Plant API that I will build. This API will include data for plants, including but not limited to the following: name, hardiness, spacing, amount of sun, amount of water, time until fruit,

### **Plant Hardiness Zone API**

https://rapidapi.com/fireside-worldwide-fireside-worldwide-default/api/plant-hardiness-zone

This app will use the **Plant Hardiness Zone API** in order to determine the hardiness zone in which the user resides. The app will then use this information to provide the user with the correct planting and care instructions for their hardiness zone.

### **WeatherAPI**

https://www.weatherapi.com/

This app will make use of the **WeatherAPI** in order to help the user properly care for their plants during various weather conditions such as extreme heat, freezes, and precipitation.

---

## Project Approach

My approach for creating the Find Musicians App will be to develop an MVP focused on the geolocation features first, and then adding the messaging features as the app evolves.

### **Database Schema**

Database models will consist of the following:

- User
- Garden
- Bed
- Plant

The User model will have a many-to-many relationship with the Garden model, so that users in the same household can share gardens, and Users can manage multiple Gardens across multiple properties.
The Garden model will have a one-to-many relationship with the Bed model, so a garden can have multiple beds throughout the property.
The Bed model will have a many-to-many relationship with the Plant model, so multiple Beds can contain the same type of Plants, and multiple Plants can be found in each Bed.

![database schema](/img/database-schema_FM.png)

### **Potential Issues**

1. In the event that the Plant Hardiness Zone API goes down, a new user should be able to manually choose a hardiness zone.  
   When a hardiness zone is set manually, there should be a state such as "hasManualHardinessZone" that will trigger the Hardiness Zone API to reset the user's hardiness zone during the next login.  
   Since the registration process will require the user's zip code, the API will be able to properly set the user's hardiness zone and set "hasManualHardinessZone" to false.
2. If the WeatherAPI is down, the user will not receive weather-related care alerts until the API is running again.

### **Security & Sensitive Information**

- User email addresses will be stored for registering a new user.
- Password security will be handled with Bcrypt.
- The app does not have any payment features to worry about.

### **Functionality**

-

### **User Flows**

User Searching for Musician
![user flow diagram](/img/user-flow_FM.png)

### **Stretch Goals**

1. Add common garden pest and pest control data
2. Add common preserving techniques for each veggie
3.
