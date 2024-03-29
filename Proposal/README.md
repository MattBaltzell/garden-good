### Capstone 2 Project Proposal

# **Garden Good App**

![GardenGood](./img/gg_logo.png)

Starting a new garden or maintaining a loved garden can be a bit overwhelming. Keeping track of your plants' varying needs essentially requires a personal assistant. Wouldn’t it be great if there was a way to handle it all yourself and have a bountiful harvest?

---

## Project Goals

The Garden Good app helps beginning gardeners and experienced gardeners plan, plant, and tend their crops for an abudant harvest. This app incorporates weather alerts to help you protect your garden from harsh conditions, and allow it to thrive. From proper feeding and watering to pruning and pests, this app will help you garden GOOD.

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
    "id": "1",
    "name": "Jalapeno",
    "species": "Capsicum annuum",
    "img_url": "https://gardengood.com/api/img/jalapeno.jpg",
    "light_id": "0",
    "is_perrenial": "false",
    "description": "Named for the town of Jalapa, Mexico, this is the most popular chile pepper in the United States. Jalapeño produces 3-inch, thick-walled, moderately hot pods with deep green color that matures to a bright red. The skin may show a netting pattern as fruit ages, but it does not affect flavor. Often, the heat of the peppers will vary, even those from the same plant. If peppers grow fast, get plenty of water, and are harvested soon, they may be milder than peppers that stay on the plant a long time, or that develop slowly and under stressful conditions. Widely adapted, jalapeño plants yield a bountiful harvest in dry or humid, hot or cool climates. The compact plants grow well in containers. Use jalapeño on nachos or in salsa, or smoke the mature red ones over mesquite chips to make your own chipotle sauce. Jalapeño became the first pepper in space when a bag full of pods accompanied astronauts on the shuttle Columbia in November 1982!",
    "days_to_maturity_min": "75",
    "days_to_maturity_max": "80",
    "instructions": {
      "planting": "Start seeds indoors 6-8 weeks before outdoor planting time for earliest harvest. Grow in sunny window. Transplant outdoors to a sunny location when seedlings have 5-6 leaves. In mild climates, may be sown directly in the garden.",
      "pruning": "Top young plants to encourage sturdier bush growth. Throughout the summer, you can optionally remove some suckers to prevent too much horizontal growth. Late in the season, prune plants heavily by cutting all shoots and side branches back by about six inches, or to a point just above the topmost fruit. Remove branches that do not hold any fruits. Finally, remove any flowers you see on the plant as well as small fruits that do not have time to ripen before the first frost.",
      "watering": "Jalapeño plants need lots of water. You should keep the soil very moist at all times. Note that dry soil can give the fruits a bitter flavor; however, you should also avoid over-saturating the soil as this could cause fungal diseases and root rot."
    }
  }
}
```

Sample API response data for a crop:

```json
{
  "crop": {
    "plant_id": "1",
    "name": "Jalapeno", //query res of `SELECT name FROM plants WHERE id = $1, [plant_id]`
    "img_url": "https://gardengood.com/api/img/jalapeno.jpg", //query res of `SELECT img_url FROM plants WHERE id = $1, [plant_id]`
    "bed_id": "7",
    "qty": "2",
    "planted_at": "2023-02-01 06:10:25"
  }
}
```

### **WeatherAPI**

https://www.weatherapi.com/

This app will make use of the **WeatherAPI** in order to help the user properly care for their plants during various weather conditions such as extreme heat, freezes, and precipitation. This API can also be used to display current weather conditions in a user's home page or nav bar.

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

### **Plant Hardiness Zone API**

https://rapidapi.com/fireside-worldwide-fireside-worldwide-default/api/plant-hardiness-zone

This app will use the **Plant Hardiness Zone API** in order to determine the hardiness zone in which the user resides. FUTURE: The app will use this information to provide the user with the correct planting dates for their hardiness zone.

Sample API response data:

```json
// GET request made with zipcode:"90210"
{
"hardiness_zone":"10b"
"zipcode":"90210"
}
```

---

## Project Approach

My approach for creating the Garden Good app will be to develop an MVP that allows the User to look up information about a Plant. For this there should be a 'plants' page that shows all plants. The user should be able to click on plant to reveal information about it. The user should also be able to search for a plant by name. Once this feature is implemented, I will add current weather data to the interface. I will also add a feature that allows Users to digitally build out their gardens. They will be able to create Garden components, add Bed components to those Gardens, and add Crop componens to those Beds.

### **Technology Stack**

- PostgreSQL
- Express
- React
- Node

### **Database Schema**

Database models will consist of the following:

- User
- Garden
- Bed
- Crop
- Plant
- Sunlight
- Season
- Instruction
- Instruction_Type
- Note

![database schema](./img/GardenGood_db-schema.png)

### **Potential Issues**

1. If the WeatherAPI is down, the user will not receive weather-related care alerts until the API is running again.
2. In the event that the Plant Hardiness Zone API goes down, a new user should be able to manually choose a hardiness zone.
   When a hardiness zone is set manually, there should be a state such as "hasManualHardinessZone" that will trigger the Hardiness Zone API to reset the user's hardiness zone during the next login.
   Since the registration process will require the user's zip code, the API will be able to properly set the user's hardiness zone and set "hasManualHardinessZone" to false.

### **Security & Sensitive Information**

- User email addresses and zip codes will be stored for registering a new user.
- Password security will be handled with Bcrypt.
- The app does not currently have a paywall or payment features, but one could be added in the future.

### **Functionality**

**Plant Care**

- Search for plant
- General plant data and care instructions

**My Garden:**

- Garden planning and organization through Garden, Bed, and Crop components
- Alerts and notifications based on weather conditions

### **User Flows**

User Flow - Find Plant Info
![user flow - find a plant](./img/gg_user-flow_find-plant.png)

User Flow - Add Crop to Bed
![user flow - add a crop](./img/gg_user-flow_add-crop.png)

### **Stretch Goals**

1. My Garden Feature
2. Add feature for users to add notes to their crops.
3. Add feature for extreme weather alerts.
4. Add feature for common garden pest and pest control data.

---

## Proposed Timeline

| **FEATURE**                              | 2/20  | 2/21  | 2/22  | 2/23  | 2/24  | 2/25  | 2/26  | 2/27  | 2/28  |  3/1  |  3/2  |  3/3  |  3/4  |  3/5  |  3/6  |  3/7  |  3/8  |  3/9  | 3/10  | 3/11  | 3/12  | 3/13  |
| ---------------------------------------- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Plant Info**                           | **x** | **x** | **x** | **x** |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
| - Backend                                |   x   |   x   |   x   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
| - Frontend                               |       |       |   x   |   x   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
| **User Auth**                            |       |       |       | **x** | **x** |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
| - Backend / Middleware                   |       |       |       |   x   |   x   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
| - Frontend                               |       |       |       |       |   x   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
| **Current Weather**                      |       |       |       |       |       | **x** | **x** |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
| - Backend                                |       |       |       |       |       |   x   |   x   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
| - Frontend                               |       |       |       |       |       |       |   x   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
| **My Gardens, Beds, Crops**              |       |       |       |       |       |       |       | **x** | **x** | **x** | **x** | **x** | **x** |       |       |       |       |       |       |       |       |       |
| - Backend                                |       |       |       |       |       |       |       |   x   |   x   |   x   |   x   |       |       |       |       |       |       |       |       |       |       |       |
| - Frontend                               |       |       |       |       |       |       |       |       |       |   x   |   x   |   x   |   x   |       |       |       |       |       |       |       |       |       |
| **FE Navigation/Routing**                |       |       |       |       |       |       |       |       |       |       |       |       |       | **x** | **x** |       |       |       |       |       |       |       |
| - Frontend                               |       |       |       |       |       |       |       |       |       |       |       |       |       |   x   |   x   |       |       |       |       |       |       |       |
| **Stretch Goal: Add Notes to Crops**     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       | **x** | **x** |       |       |       |       |       |
| - Backend                                |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |   x   |   x   |       |       |       |       |       |
| - Frontend                               |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |   x   |       |       |       |       |       |
| **Stretch Goal: Extreme Weather Alerts** |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       | **x** | **x** |       |       |       |
| - Backend                                |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |   x   |   x   |       |       |       |
| - Frontend                               |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |   x   |       |       |       |
| **Stretch Goal: Pest Control Info**      |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       | **x** | **x** | **x** |
| - Backend                                |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |   x   |   x   |   x   |
| - Frontend                               |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |   x   |   x   |
