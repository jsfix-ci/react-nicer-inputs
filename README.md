# React Nicer Inputs

An easy to use library to quickly create react forms 📝, its the new level from react-nice-inputs.

![npm](https://img.shields.io/npm/v/react-nicer-inputs)
[![React Nicer Inputs Actions Status](https://img.shields.io/github/workflow/status/wbarahona/react-nicer-inputs/%E2%9A%9B%F0%9F%8F%97%20publish?style=flat-square)](https://github.com/wbarahona/react-nicer-inputs/actions)
![David](https://img.shields.io/david/wbarahona/react-nicer-inputs)
![Snyk Vulnerabilities for npm package](https://img.shields.io/snyk/vulnerabilities/npm/react-nicer-inputs)
![NPM](https://img.shields.io/npm/l/react-nicer-inputs)

---

## Installing React Nicer Inputs

```sh
npm i -D react-nicer-inputs
```

Now import the inputs as you would regularly do by:

```js
import { Input } from 'react-nicer-inputs';
```

Now you are good to go. Create the first input as:

```js
<Input
  type="text"
  name="example"
  className="col-12 example-class"
  inputChange={({ value, name, e }) => {
    console.log(value, name, e);
  }}
  attrs={{
    placeholder: 'enter a value',
  }}
/>
```

🎇 Nice! You must now have a simple text input like so:

![simple text input](https://drive.google.com/uc?export=view&id=17mXqlbHCd3K_XPzVLcPunQkcMh48Zk7E)

And when you type in the console must display the value you type in, the name of the input and the Syntetic Event. Awesome! 😀

---

## The Components 🧰

So each component renders different inputs for you to use and each have common props which will be discussed next but for particular props check each component definition in the next section.

- `type="" {string}` This defines the type of the input being rendered, is passed to the native HTML5 type attribute; now some components do not require this or prefer the usage of a dedicated component for an specific input. Refer to each component description below what case it is for the component you are currently using.

- `name="fname" {string}` This sets the name of this input as well it is assigned to the HTML5 name and id attributes, additionally it is returned as well on the `inputChange` prop.

- `className="col-12 col-md-5" {string}` This is as you might know the class this component will have, normally the prop is assigned to the input or to the wrapper of the component such as `InputGroup`, `Password`, `Autocomplete`, `Datepicker` for example. Some components do have internal wrap blocks and those can have classNames to but the prop name might differ in each case, refer then to each component specific prop dictionary below.

  **_Observation: each input do have the `input` utility class by default so you can paint with CSS the actual input as you see fit._**

- `inputChange={} {Function}` This is the way the input return the value back. This is a semantic name for onChange (due to the implementation of TS it needed to be named as **inputChange**). You may destructure the params to:

```json
{
  e, // This is the syntetic event from the input
  name, // This is the name of the input, helpful if you are storing a model of the form in the state and you have a single function that handles input change
  value // The value from the input
}
```

- `attrs={{placeholder: 'Enter your name'}} {Object}` This is the list of HTML5 attributes the input can handle, you can send here as much as you need.

- `value={fnameVal} {string}` This is the initial value you need this input to start with, it is ignored as soon the input changes.

- `...props` Any other props from react you see you might need to pass along to the input are spreaded internally. The handle or callback is for you to write.

Now we are about to see what input components are in store for you from `'react-nicer-inputs'`.

---

### Input

As we saw in the example above this input is very helpful when you are creating classic text inputs, number, date or textarea, for the latter the input will render a proper `<textarea>` tag element. While you can create radios, checkboxes and password with this component you should favor the `<InputGroup>` component for radios and checkboxes and `<Password>` for well... pwds!

Let's see what props this component may handle in particular:

- `cols {string | number}` When you define this Input to be textarea it will handle the columns the textarea will have

- `rows {string | number}` Same as cols.

- `mask {Regex}` This prop will help the component to hide certain characters visible on the input based on a regex you provide in order to capture whatever matches on the value string and replace it with the `maskChar` value.
  For example: `mask=".{3}$"` this Regex will select the last three characters in the input and replace it with discs each character. So let's say the user types in: `reactjs` therefore the value **_VISIBLE_** will be `reac●●●` while the returned value on `inputChange` will be still string **`reactjs`**.

**_Observation: Do not missuse this functionality for a password input._**

- `maskChar {string} defaults to '●'` This prop altogether with mask allows to change the matching characters with whatever character you might need: asterisks, dashes, periods... etc.

---

### Select

This component creates a `<select>` dropdown for you. Since this is straight forward there is no more to explain for it, let's dive into the props this component use in particular aside from the common ones described above:

- `options={[ {label: 'Option 1 1️⃣', value: '1'} ]} {Array}` This is an array of objects that define the select options, additional you may send **'attrs'** a third property on each option Object. That property is spreaded on the `<option>` tag.

- `defaultLabel="Pick your favorite option" {string}` This is the default option label on the Select.

---

### InputGroup

If you need to create checkboxes and radiobutton groups this component will aid you in no time, the component renders a box with rows of radio ⏺ or checkbox ☑ inputs aside of a label for each element. So the props this input need are:

- `options={[ {label: 'Option 1 1️⃣', value: '1'} ]} {Array}` Idem as `<select>` This is an array of objects that define the select options, additional you may send **'attrs'** a third property on each option Object. That property is spreaded on the `<option>` tag.

**_Observation: This component value prop and the value returned on the inputChange function may differ wether it is a radio or checkbox_**

For checkboxes since conceptually it is a multi option selectable it will return on the inputChange function a string of the selected options separated by a commas, the same as the value prop, it will take a comma separated string of the values to be preselected by the component.

For radio buttons as its a single option selectable out of a group of option this will return on inputChange function a normal string, no commas. The value prop can be a single string of one of the options.

---

### Autocomplete

This component allows a large list of options to be browsable by typing in the textbox, reducing the ammount of options available as the user type by matching the string to any possible option.

![alt text](https://drive.google.com/uc?export=view&id=1YN8dvAaVcZ21VI8fN5InMEtLXikLw5GT)

This component needs the following props:

- `options={[ {label: 'Option 1 1️⃣', value: '1'} ]} {Array}` Idem as `<select> and <InputGroup>` This is an array of objects that define the options available to pick, from there the options are reduced as the user types in.

---

### Password

The password component is unique and helpful, following the way Edge browser allows the behavior natively to toggle show/hide the visibility of the characters on the input, this component includes a native button that allows such toggling the password to be visible or set back to be hidden.

Some props are the same as the input component but this contains the following:

- `showIcon="👁" {ReactNode} defaults to 'hide'` This is the icon to be displayed when the password is hidden
- `hideIcon="❌" {ReactNode} defaults to 'show'` This is the invers as showIcon, it displays when the password is visible
- `noToggle {boolean} defaults to false` This defines if you need the toggle button or not.

---

### Label and Feedback

These are simple components you can use to work along with any input.
The label component can take className and also requires only:

- `htmlFor="fname" {string}` This is of course the id of the input this label belongs to.

The feedback component allows to display a text and its usage is to be part of the FormGroup as a way to display messages about this input, can take className but nothing else, it will render a `<span>` element with whatever text you send to it.

---

### Datepicker

This component allows the user to select a date or a date range, depending on the `dateRange` prop the behavior of the component do change into two scenarios:

- If no `dateRange` prop is sent then it will display a single text input that when the user sets focus on displays a calendar element below, as soon as the user do select one date it will trigger the `inputChange` function and return the formatted date as value.
- If `dateRange` is sent then two inputs are displayed and the calendar accepts two dates to be selected, on each selection the component triggers the `inputChange` function but this time the value is an object like so:

```js
{
  startDate: '05-30-2021',
  endDate: '06-02-2021'
}
```

This component takes a handful of props that mutate its behavior, let's see:

- `format="DD-MM-YYYY" {string}` Allows formatting for the dates that this component will return.
- `maxDate="05-29-2021" {string}` Is the maximum date allowable to select by this datepicker
- `minDate="07-30-2021" {string}` Is the minimum date allowable to select by this datepicker
- `bottomPanel={} {Function}` Is the panel below the calendar, it prompts the user to clear selection and confirm to close calendar, must return JSX, this function can take an object as parameter, this object contains `{clearSelections, confirmSelections}` each functions can close the calendar and confirmSelections will trigger inputChange and return the value of the selected date/s. This way you return a block of JSX for further customization of the bottom panel.
- `minNights={3} {number}` Is the minimum nights allowable to select by this calendar
- `maxNights={10} {number}` Is the maximum nights allowable to select by this calendar
- `monthsToDisplay={3} {number}` Is the ammount of months to be displayed
- `disabledDates={['06-01-2021']} {Array}` Is the array of dates that this calendar will mark as unallowable to be selected
- `monthHeader={} {Function}` This allows you to create a custom header that could allow users to change months and years quickly, the function must return JSX, this function can take an object as params which contains `{ setYear, setMonth, month }`.
  - setYear is a function that takes a string of the year you want to set
  - setMonth is a function that takes a string of the month you want to set
  - month is a [momentjs](https://momentjs.com/) object that you can use to get the current month information.
- `prevButton={<JSX />} {ReactNode}` Allows to customize the navigation button for previous calendar dates
- `nextButton={<JSX />} {ReactNode}` Allows to customize the navigation button for next calendar dates
- `disableNavigationOnDateBoundary {boolean}` This prop disables the calendar navigation along with maxDate / minDate when the user has reached either the maxDate meaning that the user cant go any more into the future or cant go into the past if has reached the minDate.
- `calendarComponentClassName="col-12" {string}` Is the class that the calendar wrapper(which contains the month/months, navigation arrows... etc) below the input can have
- `calendarClassName="col-12 col-md-6" {string}` Is the class that each of the months can have, allows for further customization on each of the months wrappers

---

### Calendar

This is a calendar element that you can use to make your own implementations of date picker without the `<DatePicker>` component in favor of your own ways.
All the props explained in the `<DatePicker>` component are almost the same.

- `className="custom-calendar" {string}` This class is appended to the wrapper of this calendar component.
- `calendarClassName="col-12 col-md-4" {string}` Is the class that each of the months can have, allows for further customization on each of the months wrappers

---

### DropDownDates

This component is kinda special, sometimes somewhere there is the need to select a date in a very unique way. Selects. Yep! So, we got you covered, here this component renders three different selects for each of the segments of the date, month, day and year. The value of each select depends of the props as well. Let's take a peek:

- `format="DD-MM-YY" {string}` Allows formatting for the dates that this component will return.
- `maxDate="05-29-2021" {string}` Is the maximum date allowable to select by this datepicker
- `minDate="07-30-2021" {string}` Is the minimum date allowable to select by this datepicker
- `ddClassName="col-3" {string}` This className is appended to the wrapper of the Day selector
- `mmClassName="col-3" {string}` The same as day selector
- `yyClassName="col-6" {string}` The same as day selector
- `ddLabel="Pick day:" {string}` This is the text of the `<label>` element above the day `<select>`
- `mmLabel="Pick month:" {string}` The same as day Label
- `yyLabel="Pick year:" {string}` The same as day Label
- `ddDefaultLabel="Day..." {string}` This prop allows to customize the default text on the `<Select>` component
- `mmDefaultLabel="Month..." {string}` The same as Day Default Label
- `yyDefaultLabel="Year..." {string}` The same as Day Default Label
- `displayOrder="DD-MM-YYYY" {string}` This allows to customize the order of rendering of each selector
- `mmmm {boolean}` If you need the month element to have words instead of numbers

**_Observation: The options react to maxDate and minDate and its options are rerendered to disallow user selecting dates out of boundaries._**

---

### Form Group

This is a component that is composed of three elemental components.

```html
<label>
  <input /> ||
  <select>
    ||
    <InputGroup>
      ||
      <AutoComplete>
        ||
        <DatePicker>
          ||
          <Password> <Feedback></Feedback></Password></DatePicker></AutoComplete
    ></InputGroup></select
></label>
```

So, it utilizes all the props explained for each component above.

---

## CODE SANDBOX 🛠

Have a spin: check this **_codesandbox_**

[![Edit quiet-tdd-97si6](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/quiet-tdd-97si6?fontsize=14&hidenavigation=1&theme=dark)
