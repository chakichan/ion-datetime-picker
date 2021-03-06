# ion-datetime-picker
> Date and/or time picker for awesome [Ionic framework](http://ionicframework.com/) v1

# Introduction

This component was originally made by [katemihalikova](https://github.com/katemihalikova/ion-datetime-picker). This fork was made because of recent changes in Google Chrome 67's way
of handling historic timezones.

# Features

The ion-datetime-picker component has these features:
- Make Date picker, Time picker, Datetime picker
- Choose Sunday or Monday as the first day of the week
- Use 12-hour or 24-hour clock
- Pick time with or without seconds
- Configure popup title and button labels and classes
- Configure i18n to get weekdays and months in your language
- Configure size of a step

# Usage

Put the `ion-datetime-picker` directive alongside the `ng-model` wherever you want to tap to show the picker:

```html
<ion-list>
  <div class="item" ion-datetime-picker ng-model="datetimeValue">
    {{datetimeValue| date: "yyyy-MM-dd H:mm:ss"}}
  </div>
</ion-list>
```

*It is not possible to use `<ion-item>` until [#18](https://github.com/katemihalikova/ion-datetime-picker/issues/18) is fixed.*


## Configuration attributes

### `date` and `time` attributes

Choose which picker type is used. When neither is set, I assume both and use the datetime picker.

### `monday-first` attribute

Set this if you want to have Monday as the first day of a week.

### `seconds` attribute

By default, in the time picker, I allow to change only hours and minutes. Set this attribute to use also seconds.

### `am-pm` attribute

By default, in the time picker, I use 24-hour clock. Set this attribute to change it to 12-hour clock.

### `month-step`, `hour-step`, `minute-step` and `second-step` attributes

By default, when any caret button is tapped, I add or subtract 1 particular unit. Set these attributes to change it to anything you want.

### `title` and `sub-title` attributes

Configure the title and sub title of the popup with the picker.

_HINT: Use `data-title` instead of `title` if you are going to use the app in the desktop browser to prevent leaking of the text into a mouseover tooltip._

### `button-ok` and `button-cancel` attributes

Configure the text of buttons at the bottom of the picker.

### `only-valid` attribute

Disable/Enable calendar days according to type and date range specified.

```html
only-valid="{'after': '2016-04-09'}"
only-valid="{'after': 'today', 'inclusive': true}"
only-valid="{'outside': {'initial': '2016-04-09', 'final': '2016-06-15'}, 'inclusive': true}"
```

Types supported: `'after'`, `'before'`, `'between'` and `'outside'`. If you want to include the day specified, set `'inclusive'` property to `true`.

To combine rules, just pass an array and it should do the trick. Rules are complementary (treated with AND, not OR), it means that a date will be available only if it matches all the constraints you pass.

```html
only-valid="[{'after': '2017-01-12'}, {'outside': {'initial': '2017-01-19', 'final': '2017-01-29'}}, {'outside': {'initial': '2017-02-19', 'final': '2017-02-29'}}]"
```

## Internationalization & customization factory

Simple internationalization & customization options. Inject the `$ionicPickerI18n` factory into your code and set the localized strings and button classes.

### `weekdays` key

Array of weekdays abbreviations. `0` is Sunday. If `moment` is installed, I try to get localized data from it, otherwise English ones are used as default.

### `months` key

Array of months names. `0` is January. If `moment` is installed, I try to get localized data from it, otherwise English ones are used as default.

### `ok` and `cancel` keys

Default, global labels of the buttons at the bottom of the picker.

### `okClass`, `cancelClass` and `arrowButtonClass` keys

Custom space-delimited classes applied to the buttons at the bottom of the picker.

```js
angular.module("myApp")
  .run(function($ionicPickerI18n) {
    $ionicPickerI18n.weekdays = ["Нд", "Lu", "Út", "Mi", "To", "금", "Sá"];
    $ionicPickerI18n.months = ["Janvier", "Febrero", "März", "四月", "Maio", "Kesäkuu", "Červenec", "अगस्त", "Вересень", "Październik", "Νοέμβριος", "డిసెంబర్"];
    $ionicPickerI18n.ok = "オーケー";
    $ionicPickerI18n.cancel = "Cancelar";
    $ionicPickerI18n.okClass = "button-positive";
    $ionicPickerI18n.cancelClass = "button-stable";
    $ionicPickerI18n.arrowButtonClass = "button-positive";
  });
```

## Daylight saving time

The datetime picker is using `Date` object with your browser's timezone, including any DST. When you change the date, hour, minute, or second, which sets the time to an invalid value because of moving from 2:00 to 3:00 at the beginning of DST, the time is automatically adjusted to a valid value. On the other hand, when the DST ends, I do NOT take the inserted hour into consideration, but this may be fixed in the future.

# More info

For more info, check the [original plugin](https://github.com/katemihalikova/ion-datetime-picker).