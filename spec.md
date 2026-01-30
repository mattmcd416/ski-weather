I want to build a single-page, static HTML site that .

My goal is to build a simple page that will help me determine the best mountain to ski at on a certain date range.

Requirements:
- single-page
- static HTML
- use jQuery as the only javascript dependency
- store all data in local browser storage (such as collection of mountains)
- UI should have a top-level form that stays sticky to the top of the page. this form should contain:
    - A date range picker (start/end date)
    - Buttons to populate the date range with this weekend + next weekend
        - `weekend` here means the upcoming friday, saturday and sunday
        - the date picked should default to the next upcoming weekend (the equivalent of clicking "this weekend")
    - The ability to specify the elevation to fetch weather for (should have a drop-down for Base, Mid-Mountain, and Peak, with Mid-Mountain as the default)
    - All of these form elements should be side by side
    - A "Load Forecast" button that when clicked, shows a progress bar as weather data is being fetched
- A "Mountain Manager" UI Box - allows for CRUD operations of mountains
    - Each mountain effectively has the following fields:
        - lat
        - lng
        - base elevation (ft)
        - peak elevation (ft)
        - (calculated) mid mountai elevation [(peak - base / 2)]
    - A table of all mountains being forecast, including all of their fields
    - Button to delete an individual mountain
    - Button to edit field like lat, lng, elevations etc.
    - Special button to add all Epic Northeast mountain
- Upon clicking the aforementioned "Load Forecast" button:
    - Data fetching: each mountains weather should be fetched from open-meteo.com APIs
        - use the specified base/mid/peak for temp and wind values
        - (fetch all 3 elevations and show the respective one when the base/mid/peak dropdown changes)
    - AN overall winner box with a list of pros/cons (why it's the overall best choice for the time range)
        - pros should reference specific metrics that are in desirable ranges like high snowfall, high temperature, low wind speeds, high visibility
        - cons should include  specific things like not-desirable ranges like low snowfall, rain, ice, low temperatures, high wind speeds, low visibility
    - 1 "box" per day of the specified date range, each box should contains:
        - A heading for the box with
            - the date (aka `Saturday, Jan 31`)
            - the "winning" mountain
            - the pros and cons of the winning mountain (why it was chosen)
        - A table that compares each mountain with the following columns:
            - Mountain (name)
            - Score (a value of 0-100 that scores the mountain based on how favorable the conditions are to ski.. feel free to take a first attempt at a formula)
            - Feels Like / Apparent temperature range (min-max)
            - Actual temperature range (min-max)
            - Wind speed range (min-max)
            - Max wind gust speed
            - Wind direction (use W, NW, etc. instead of # of degrees)
            - number of inches of snow
            - number of inches of rain
            - number of inches of ice
            - ALL MIN/MAX VALUE METRICS SHOWN IN THIS TABLE SHOULD OCCUR DURING 9am-4pm "ski time window"
        - A series of side by side graphs (each one should take ~ 50% of the page width):
            - line graphs, 1 mountain per series
                - apparent/Feels-like temperature
                - actual temperature
                - wind speed
                - max wind gust speed
                - cloud cover
                  -visibility
            - bar/column charts, 1 mountain per column (y-axis = number of inches, x-axis = 1 bar per mountain)
                - inches of snow
                - inches of rain
    - IMPORTANT: Clicking ANY of the chart series should effectively "solo" that series (hide others), not just on the clicked chart, but ALL charts on the page
    - IMPORTANT: all charts should have a "ski day" shaded area from 9am-4pm
    - IMPORTANT: all charts that share a same y-axis (such as temperature and feels-like or the combination of wind speed and wind gusts) should have the same SCALE of
    - IMPORTANT: the per-day tables should have column headings at the TOP of the table, indicating the measurement and SPECIFY THE UNITs (aka °F or mph)
      that axis
    - IMPORTANT: all charts should have roughly a 4:3 width/height ratio and take up ~ 40% of the screen (height)
    - When scrolling
        - the overall / top form (date + base/mid/peak selection) should stay "sticky" at the top
        - the per-day box heading should be sticky until you scoll past it
        - the per-day table column headins be sticky until you scoll past it
- Bonus: ability to specify units (F vs C for temp, mph vs kmph for wind, ft vs m for elevation)
    - preferences saved in local storage
    - fetch the last week of historic data and look for "freeze thaw" cycles where the temperature goes from feezing to over freezing and back to freezing
        - add a column to show the number of freeze thaw cycles in the last 7 days in the table that compares each mountain
        - IMPORTANT: when fetching the last 7 days of weather data, be sure to just adjust the overall date range to fetch weather for as the API doesn't support past days
- Any errors (such API request failures) should trigger a popup with the error
- The Page should have very minimal margins on the left and right side
- Things to watch out for:
    - Open-Meteo API is a bit picky: if you request even one variable that doesn't exist in their specific forecast model, the whole request fails
        - Specifically, ice_pellets and showers are not standard hourly variables in their basic forecast API. swap those out for the standard variables (precipitation, rain, snowfall) and updated the scoring logic to reflect the available data.
        - adjust the URL construction to ensure the elevation value is an integer, as decimals can sometimes trip up their parser.
- use emojis with text to make it cute/playful
- IMPORTANT: for layout, the "mountain manager" each section (top menu, mountain manager, results) should be taking up most of the width of the page and occur one after another

IMPORTANT: BE SURE TO CONSIDER ALL REQUIREMENTS AND INCLUDE ALL Epic Mountains in NH and VT including:
- Stowe Mountain Resort (VT)
- Okemo Mountain Resort (VT)
- Mount Snow (VT)
- Wildcat Mountain (NH)
- Attitash Mountain Resort (NH)
- Mount Sunapee Resort (NH)
- Crotched Mountain (NH)

BE SURE TO include ALL SPECIFIED CHARTS AND TABLE COLUMNS!

please include the entire single page html with each reply