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

Sample API response data for a user:

```json
{
  "user": {
    "username": "mattbaltzell",
    "first_name": "Matt",
    "last_name": "Baltzell",
    "email": "matthew.j.baltzell@gmail.com",
    "zip_code": "36830",
    "hardiness_zone": "8a",
    "created_at": "2023-02-01 06:10:25",
    "last_login_at": "2023-02-03 10:24:02",
    "gardens": []
  }
}
```

Sample API response data for a plant:

```json
{
  "plant": {
    "id": "23",
    "name": "Habanero",
    "species": "Capsicum chinense",
    "description": "The habanero is a hot variety of chili. Unripe habaneros are green, and they color as they mature.The most common color variants are orange and red, but the fruit may also be white, brown, yellow, green, or purple. Typically, a ripe habanero is 2–6 centimeters (3⁄4–2+1⁄4 inches) long. Habanero chilis are very hot, rated 100,000–350,000 on the Scoville scale. The habanero's heat, flavor and floral aroma make it a popular ingredient in hot sauces and other spicy foods.",
    "days_to_maturity": "90",
    "instructions": {
      "planting": {},
      "pruning": {},
      "watering": {},
      "pest_control": {}
    }
  }
}
```

Sample API response data for a crop:

```json
{
  "crop": {
    "plant_id": "23",
    "name": "Habanero", //query res of `SELECT name FROM plants WHERE id = $1, [plant_id]`
    "img_url": "https://gardengood.com/api/img/habanero.jpg", //query res of `SELECT img_url FROM plants WHERE id = $1, [plant_id]`
    "bed_id": "7",
    "qty": "2",
    "planted_at": "2023-02-01 06:10:25",
    "notes": "Grew extremely well this year due to being placed in the middle of the garden. 40% more yeild than last year!"
  }
}
```

### **Plant Hardiness Zone API**

https://rapidapi.com/fireside-worldwide-fireside-worldwide-default/api/plant-hardiness-zone

This app will use the **Plant Hardiness Zone API** in order to determine the hardiness zone in which the user resides. The app will then use this information to provide the user with the correct planting and care instructions for their hardiness zone.

Sample API response data:

```json
// GET request made with zipcode:"90210"
{
"hardiness_zone":"10b"
"zipcode":"90210"
}
```

### **WeatherAPI**

https://www.weatherapi.com/

This app will make use of the **WeatherAPI** in order to help the user properly care for their plants during various weather conditions such as extreme heat, freezes, and precipitation.

Sample API response data for a daily forcast:

```json
{
  "forecast": {
    "forecastday": [
      {
        "date": "2023-02-03",
        "date_epoch": 1675382400,
        "day": {
          "maxtemp_c": 14.1,
          "maxtemp_f": 57.4, // will use maxtemp_f to check if user should be alerted to water their plants and/or use shade cloth to protect plants from burning
          "mintemp_c": 4.3,
          "mintemp_f": 39.7, // will use mintemp_f to check if user should be alerted to protect their plants from frost
          "avgtemp_c": 9.0,
          "avgtemp_f": 48.2,
          "maxwind_mph": 11.9,
          "maxwind_kph": 19.1,
          "totalprecip_mm": 13.7,
          "totalprecip_in": 0.54, // will use totalprecip_in along with maxtemp_f to check if user should be alerted to water their plants or not
          "totalsnow_cm": 0.0,
          "avgvis_km": 9.4,
          "avgvis_miles": 5.0,
          "avghumidity": 67.0,
          "daily_will_it_rain": 1,
          "daily_chance_of_rain": 88,
          "daily_will_it_snow": 0,
          "daily_chance_of_snow": 0,
          "condition": {
            "text": "Moderate rain",
            "icon": "//cdn.weatherapi.com/weather/64x64/day/302.png",
            "code": 1189
          },
          "uv": 2.0
        }
      }
    ]
  }
}
```

---

## Project Approach

My approach for creating the Garden Good App will be to develop an MVP that allows the User to look up information about a Plant. For this there should be a 'plants' page that shows all plants. The user should be able to click on plant to reveal information about it. The user should also be able to search for a plant by name. Once this feature is implemented, I will add a feature allowing Users digitally build out their gardens. They will be able to create Garden components, add Bed components to those Gardens, and add Crop componens to those Beds.

### **Database Schema**

Database models will consist of the following:

- User
- Garden
- Bed
- Crop
- Plant
- Instruction
- Instruction_Type
- Hardiness_Zone

![database schema](./img/GardenGood_db-schema.png)

### **Potential Issues**

1. In the event that the Plant Hardiness Zone API goes down, a new user should be able to manually choose a hardiness zone.
   When a hardiness zone is set manually, there should be a state such as "hasManualHardinessZone" that will trigger the Hardiness Zone API to reset the user's hardiness zone during the next login.
   Since the registration process will require the user's zip code, the API will be able to properly set the user's hardiness zone and set "hasManualHardinessZone" to false.
2. If the WeatherAPI is down, the user will not receive weather-related care alerts until the API is running again.

### **Security & Sensitive Information**

- User email addresses and zip codes will be stored for registering a new user.
- Password security will be handled with Bcrypt.
- The app does not currently have a paywall or payment features, but one could be added in the future.

### **Functionality**

**Plant Care**

- Search for plant
- General plant data
- Plant care instructions adjusted for User hardiness zone

**My Garden:**

- Garden planning and organization through Garden, Bed, and Crop components
- Alerts and notifications based on weather conditions

### **User Flows**

User..
![user flow diagram]() - Coming Soon

### **Stretch Goals**

1. Add common garden pest and pest control data
2. Add common preserving techniques for each veggie
3. Add bed building techniques to help new gardeners get started (tips like leave room to walk and dont make the bed bigger than you can reach) maybe this can have a user add feature where people can suggest ideas and share experiences
4. Building plans for different types of garden beds
