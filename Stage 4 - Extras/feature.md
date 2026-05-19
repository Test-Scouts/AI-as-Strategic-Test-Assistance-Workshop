create automatic test cases for this feature:

Feature: Route Planning with POIs
  In order to plan an efficient and comfortable long-distance trip
  As a driver
  I want the system to calculate a route with charging stops and nearby amenities
  Scenario: Plan a trip with specific POI category and distance constraint
    Given the trip planner is expanded
    When I enter "Stureplan, Stockholm" as the starting point
    And I enter "Linköping" as the destination
    And I enable the "Restaurant" POI filter
    And I set the "Max distance to POI" slider to "200m"
    And I click "Plan Route"
    Then the route calculation should prioritize charging stations that have a restaurant within 200m