# Data
## Fields
### ``vehicle_trip_data.csv``
* ``dev_id``: ID for the vehicle
* ``dst``: total distance driven by that vehicle
* ``spd``: current speed of the vehicle
* ``cns_tot``: total consumption for that vehicle
* ``cns_rmg``: remaining tank capacity, in percentage

### ``vehicle_trip_data_valset.csv``
* ``dev_id``: ID for the vehicle
* ``cap``: evaluated tank capacity for the vehicle

# Use Cases
## Derive tank capacities
### Calculate the overall average consumption
$ cns_tot_avg = cns_tot / dst $

### Calculate the actual consumption for the last few trips
1. Derive the last trip for every single vehicle
When the time goes backwards for a given vehicle, the remaining tank capacity increases,
up until it goes back to a lower value. The actual consumption is the capacity change
divided by the distance change.


