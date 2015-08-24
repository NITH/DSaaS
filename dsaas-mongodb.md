# MongoDB format for storing and querying data from the internet of things

This nesting can continue virtually forever to store more data points per (interval).

# integration_id

The integration_id is the identity of the data source (i.e., sensor) that provided the data points for the given interval (in this case, day (24 hours)).

# date

The date of the current measurement, used to query the database. The format of this does not matter as long as it is reflected in code.

# last_value

last_value is a simple cache used to quickly look up the last value for dashboards that only care for this value. This proved very useful for the dashboard, which only showed the previously recorded value.

## time

The time of recording.

## value

The recorded value.

# data

All of the recorded data for the "outer" interval (in this case, date).

The structure assumes that only one data point will be collected per minute per hour, and that data will be gathered continuously. It does not account for missing data. If more or less frequent data points are required, however, it is easy to expand or reduce: the easiest way is to simply reduce or add to the number of points within each minute, but one could also further nest the data. For example, to gather _five_ data points per _second_, the new data structure could look as follows:

```js 
'data': {
  '00': { // hour with 60 minutes
    '00': [0, 0, 0, 0, 0], // minute with 5 data points
    '01': [0, 0, 0, 0, 0], // minute with 5 data points
    '02': [0, 0, 0, 0, 0], // minute with 5 data points
    // ... and so on
  },
  '01': {
    // ...
  },
  // ... and so on
}
```

