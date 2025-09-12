# ResortPass Mobile Developer Interview Test

## Delivery Method 🚚

Candidates should create a fork from the following repository: https://github.com/resortpass/mobile-interview-test. You'll then open one single pull request (PR) from your fork containing all the changes, including the initial project scaffolding and the implementation of the test.

Candidates have 5 days from the day they receive the test to deliver it.

Candidates should also write a README file on their fork with a brief explanation of how their architecture works and any other important aspects of the project.

Candidates have **5 days** from the day they receive the test to deliver it.

Candidates should also write a **README** file on their fork with a brief explanation of how their architecture works and any other important aspects of the project.

## The test

Welcome to the technical evaluation for the Flutter Developer position at ResortPass. This test is designed to assess your practical skills and understanding of mobile application development principles using the Flutter framework. Please read the instructions and requirements carefully before you begin.

### Evaluation Criteria

We will review your project based on the following key aspects of software development:

- **Architecture and Code Structure:** We will analyze how you structure your code, organize different layers of your application, and manage dependencies.
- **State Management:** Your approach to handling the state of the application will be evaluated, with a focus on efficiency and maintainability.
- **API Interaction and Error Handling:** We will assess how you execute API calls, handle asynchronous operations, and manage various response states and potential errors.
- **Data Serialization/Deserialization:** The methods you use to convert data between JSON and Dart objects will be reviewed.
- **Dependency Injection:** We will look at your use of dependency injection patterns to build a modular and testable application.
- **Navigation:** Your solution for handling navigation between different screens will be evaluated for its clarity and robustness.
- **Code Readability and Documentation:** Your solution must be easy to read, with clear and consistent naming conventions. We will also review whether your code is documented with meaningful comments that explain complex logic, design choices, or non-obvious decisions.

### Technical Requirements

To ensure a consistent evaluation process, please adhere to the following technical requirements:

- **Flutter Version:** Your project must be built with a minimum Flutter version of `3.32.0`.
- **State Management:** You are required to use the `flutter_bloc` package for state management.
- **Target Platforms:** The project should be configured to run on both Android and iOS, and the implementation must function normally on both platforms.
- **API Calls:** You are free to choose your preferred method for handling API calls, whether using a third-party package or the built-in `http` library.
- **Dependency Injection:** We recommend using the `get_it` package, but you are free to use any dependency injection solution you prefer.

### Bonus Points

The following items are not mandatory but will be considered a significant plus in our evaluation:

- **Image Caching:** Implement a solution for image caching. The application should cache images on the first load and use the cached version upon content refresh, avoiding unnecessary re-downloads.
- **UI/UX Best Practices:** Demonstrate an organized approach to managing your UI components, including typography, spacing, colors, and border radii. We will inspect how you organize your UI kit.

### The Task

The task consists of building two interconnected screens that perform API calls and display the results.

#### Screen 1: Autocomplete Search

The primary goal of this screen is to provide a search functionality, where the application suggests a list of places as the user types a search term.

#### Requirements

- **Content:** The screen must have a top header containing a search bar. The main body should display a dynamic list of places returned by the API.
- **State Handling:** The screen must properly handle and display:
    - **Empty States:** When no results are returned for a search.
    - **Error States:** When an API call fails.
- **Search Logic:**
    - You will call the API by passing the typed search terms as a query parameter.
    - **Debouncing:** The API call must be debounced. A new request should only be made 500 milliseconds after the user's last keystroke.
    - **Cancellation:** Before initiating a new API call, the previous one must be cancelled.
    - **Loading State:** A loading state should be clearly indicated while the API call is in progress. You can use a loading indicator within the search bar's prefix icon or an alternative visual cue.

#### API Endpoint

The API to be used for this screen is a `GET` request to:

`https://staging-app.resortpass.com/api/search/places/autocomplete?terms={terms}&limit=10&offset=0`

Sample response:
```json
[
    {
        "id": 236,
        "name": "Newport Beach, California",
        "type": "city",
        "detailed_type": "city",
        "url": "/hotel-day-passes/Newport-Beach-236",
        "parent_id": 4,
        "parent_type": "state",
        "state_code": "CA",
        "country_code": "US",
        "city_name": "Newport Beach",
        "latitude": 33.6189,
        "longitude": -117.9298,
        "distance_search_only": false,
        "indexName": "staging_locations",
        "objectID": "Newport Beach, California",
        "queryID": "6bfbd2b0055720ff3a0a13d6a96775bc"
    },
    ...
]
```

#### Screen 2: Hotel Listings

This screen will display a list of hotels based on the place selected from the autocomplete search results on Screen 1.

#### Requirements

- **Data Source:** The screen will use the latitude and longitude of the selected place to call the next API.
- **Rendering:** You are required to render the results in a vertical list, following a clean and professional design.
- **State Handling:** Similar to Screen 1, the screen must properly handle and display:
    - **Empty States:** When no hotels are available for the given location.
    - **Error States:** When the API call fails.
- **Loading State:** A clear loading state should be displayed while the API call is in progress.

#### API Endpoint and Request Body

The API for this screen is a `POST` request to:

`https://staging-app.resortpass.com/api/search/algolia_hotels_v7`

The body of the request must be a JSON object in the following format:

```json
{
    "location":
    {
        "latitude": 40.757,
        "longitude": -73.736
    },
    "limit": 30,
    "offset": 0
}
```

Sample response:
```json
{
    "stage": 1,
    "total": 164,
    "pages": 6,
    "page": 0,
    "hits_per_page": 30,
    "offset": 0,
    "limit": 30,
    "queryID": "61273775fca35824ba5f7be382029afc",
    "indexName": "staging_hotels_v3",
    "currency": {
        "id": 7,
        "symbol": "$",
        "name": "United States Dollar",
        "iso_code": "USD",
        "created_at": "2022-01-10T10:52:09.456-05:00",
        "updated_at": "2022-01-10T10:52:09.456-05:00",
        "active": true
    },
    "user_from_usa": true,
    "hot_spot_hotels": [],
    "hotels": [
        {
            "active": true,
            "adults_only": false,
            "allow_booking": "0",
            "amenities": [
                {
                    "description": "Food Service",
                    "icon_text": "e908",
                    "name": "food"
                },
                ...
            ],
            "availability": true,
            "avg_rating": 0.0,
            "cancellation_window": 840,
            "can_be_cancelled": true,
            "city_id": 123,
            "city_name": "New York",
            "city_sort_order": 1,
            "closed_for_season": false,
            "code": "NY",
            "country": "United States of America",
            "country_code": "US",
            "created_at": "2023-07-06",
            "desktop_img": "https://assets-staging.resortpass.dev/uploads/image/picture/35445/TWA_pool7.jpg",
            "discounted": false,
            "distance_text": "",
            "distance_miles": 8.0,
            "hotel_star": 4,
            "hotels_count": 31,
            "id": 1990,
            "image": [
                {
                    "picture": {
                        "url": "/uploads/image/picture/35445/TWA_pool7.jpg",
                        "results": {
                            "url": "https://assets-staging.resortpass.dev/uploads/image/picture/35445/results_TWA_pool7.jpg"
                        },
                        "details": {
                            "url": "https://assets-staging.resortpass.dev/uploads/image/picture/35445/details_TWA_pool7.jpg"
                        }
                    }
                },
                ...
            ],
            "is_usa": true,
            "latitude": 40.6457482,
            "longitude": -73.7780172,
            "name": "TWA Hotel",
            "objectID": "1990:3227034",
            "offers": [],
            "product_categories": [
                "Pool"
            ],
            "product_id": 3227034,
            "product_images": [],
            "product_name": "Pool Pass 9pm-10:45pm",
            "product_type_id": 2,
            "products": [
                {
                    "availability": "available",
                    "id": 3227029,
                    "name": "Day Pass",
                    "price": 50.0,
                    "product_categories": [
                        "Pool"
                    ],
                    "product_type_id": 2,
                    "product_type_name": "Day Pass",
                    "product_type_sort_order": 1,
                    "quantity": 30,
                    "show_currency": false
                }
            ],
            "rating": 4.1,
            "region": [
                "new-york-city"
            ],
            "reopen_date": null,
            "reviews": 164,
            "short_desc": "Provide discuss attention. Until however think top reduce fire. Mouth job source feel over town modern.",
            "sort_order": 10,
            "state": "New York",
            "state_code": "NY",
            "state_id": 38,
            "timezone": "US/Eastern",
            "url": "twa-hotel",
            "vibes": {
                "primary": "Trendy",
                "secondary": null
            },
            "_geoloc": {
                "lat": 40.6457482,
                "lng": -73.7780172
            }
        },
        ...
    ]
}
```

We look forward to reviewing your solution. Good luck!
