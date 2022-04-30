# Driver-Capacity-Mapping
This repo takes the input of hourly order forecasts, potential utilization, and worker's shift structure of each express warehouse and returns the driver capacities to be used at each express warehouse for the period of forecast. 

## File Structure
1. **constants.py**: User is expected to provide the path to _hourly forecast orders_,  _potential utilizaiton_ , _requested buffers in capacities (optional)_ in this file for starters.
2. **requirements.txt**: This lists the neccessary dependencies by the repo.
3. **helpers.py**: User isn't expected to interact with this file. It contains the methods of data extraction, process, and shift mapping.
4. **run.py**: After setting up constants, user is expected to only run the run.py file from main to get output on _output_path_.

## Sample Views:
A few sample views of inputs of _hourly_order_forecast_, _potential_utilization_ are attached under _sample_inputs_file_

## Logic Overview:
The repo is taking the forecast orders and converting into the required riders at each hour. Once a list of required riders is created, _Google OR Tool's Constraint Programming module_ is used to come up with most optimal capacities.

At a very high level, this how the inputs of optimization looks like:
1. **Variable**- The capacities at each shift (Shifts are created at run time with the user input)
2. **Constraints**- The sum of riders present in each unique shift hour slot should be greater than or equal to the riders required in similar shift hours
3. **Objective**- Minimize the sum of all capacities allocated for each EW for each day.
