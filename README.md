# React Native Dates

__React Native Date and date range picker / calendar for iOS and Android__

Based on https://github.com/werein/react-native-dates

## API

```javascript
type DatesType = {
  range: boolean, // select a range of dates
  history: boolean, //allow dates in the past to be selected
  date: ?moment,
  startDate: ?moment,
  endDate: ?moment,
  focusedInput: 'startDate' | 'endDate',
  onDatesChange: (date: { date?: ?moment, startDate?: ?moment, endDate?: ?moment }) => void,
  isDateBlocked: (date: moment) => boolean
}
```

## Demo

<img src="http://i.giphy.com/YUqyKQoeNs2v6.gif">
<img src="http://i.giphy.com/130cHgOE0K5TCU.gif">


## Example

In this example we disabled dates back in history and on Sundays and showed selected date bellow

```javascript
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 * @flow
 */

import React, { Component } from 'react';
import {
  AppRegistry,
  StyleSheet,
  Text,
  View
} from 'react-native';
import Dates from 'react-native-dates';

export default class ReactNativeDatesDemo extends Component {
  state = {
    date: null,
    focus: 'startDate',
    startDate: null,
    endDate: null
  }


  render() {
    const isDateBlocked = (date) =>
      date.format('dddd') === 'Sunday';

    const onDatesChange = ({ startDate, endDate, focusedInput }) =>
      this.setState({ ...this.state, focus: focusedInput }, () =>
        this.setState({ ...this.state, startDate, endDate })
      );

    const onDateChange = ({ date }) =>
      this.setState({ ...this.state, date });


    return (
      <View style={styles.container}>
        <Dates
          onDatesChange={onDatesChange}
          isDateBlocked={isDateBlocked}
          startDate={this.state.startDate}
          endDate={this.state.endDate}
          focusedInput={this.state.focus}
          history={true}
          range
        />

        <Dates
          date={this.state.date}
          onDatesChange={onDateChange}
          isDateBlocked={isDateBlocked}
        />

      {this.state.date && <Text style={styles.date}>{this.state.date && this.state.date.format('LL')}</Text>}
      <Text style={[styles.date, this.state.focus === 'startDate' && styles.focused]}>{this.state.startDate && this.state.startDate.format('LL')}</Text>
      <Text style={[styles.date, this.state.focus === 'endDate' && styles.focused]}>{this.state.endDate && this.state.endDate.format('LL')}</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexGrow: 1,
    marginTop: 20
  },
  date: {
    marginTop: 50
  },
  focused: {
    color: 'blue'
  }
});

AppRegistry.registerComponent('ReactNativeDatesDemo', () => ReactNativeDatesDemo);
```
