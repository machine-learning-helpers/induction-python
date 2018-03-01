# Data
## Fields
* ``customer_id``: customer identifier. A given customer may have made several trips. All the trips of a given customer will appear in the dataset.
* ``driver_id``: driver identificator. A given driver may have made several trips. The dataset does not give all the trips for a given driver.
* ``creation_date``: date-time of the booking for the trip.
* ``booking_source``: type of application for the booking (eg, Android/IOS, web/mobile web).
* ``car_type``: car type (eg, economical, luxury, minivan).
* ``estimated_distance``: calculated distance, in km, between pick-up and drop-off locations. When empty, it means that the customer did not specify the drop-off location.
* ``distance_travelled``: actual distance, in km, measured once the trip has completed.
* ``distance_travelled_while_moving``: distance, in km, for the fast portion of the trip (eg, not stuck in traffic)
* ``estimated_duration``: estimated duration, in mn, of the trip. When empty, it means that the customer did not specify the drop-off location.
* ``duration_time``: actual duration, in mn, for the trip after its completion.
* ``wait_time_initial``: duration, in mn, for the driver waiting for the customer to show up at the pick-up location.
* ``wait_time_in_journey``: duration, in mn, for the slow portion of the trip (eg, stuck in traffic)
* ``estimated_price``: estimated price of the trip. When empty, it means that the customer did not specify the drop-off location.
* ``price``: actual price for the trip after its completion.
* ``is_cancelled``: whether or not the trip was cancelled.
* ``rating``: rating (raning from 0 to 5) of the customer for the trip.
  * 0 means that there is no data.
  * 1 is the minimal rating
  * 5 is the maximal rating
* ``was_rated``: whether or not the customer rated the trip
