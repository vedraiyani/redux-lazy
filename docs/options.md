# Options

When you add action you can set the 3rd parameter - options

```javascript
rl.addAction('title', payload, options);
```
## isEvent

If you are using **[redux-observable](https://redux-observable.js.org/)** you need to send events to epics.
Each event action should have only the type without any other fields.

```javascript
rl.addAction('event', {}, { isEvent: true });
```
The same result you can get using addEventAction:

```javascript
rl.addEventAction('event');
```

## isForm

When you need action to submit form you need to run event.preventDefault.
To make this you can wrap function:

```javascript
rl.addAction('submit');
```

And put as props:

```html
<form onSubmit={(event) => {
    event.preventDefault();
    props.submitAction();
}}>
```

Or you can use **isForm** option:

```javascript
rl.addAction('submit', {}, { isForm: true });
```

And put as props:

```html
<form onSubmit={props.submitAction}>
```

The same result you can get using addFormAction:

```javascript
rl.addFormAction('submit');
```

## isFormElement

When you need action to get value from form input event (event.target.value):

```javascript
rl.addAction('title', { title: '' });
```

And put as props:

```html
<input
  type="text"
  onChange={event => props.titleAction(event.target.value)}
  value={props.title}
/>
```
Or you can use **isFormElement** option:

```javascript
rl.addAction('title', { title: '' }, { isFormElement: true });
```
And put as props:

```html
<input
  type="text"
  onChange={props.titleAction}
  value={props.title}
/>
```

## asParams

Each time to run action you need to put payload as object:

```javascript
rl.addAction('title', { title: '' });
const { actions } = rl.flush();
```
And you will have action:

```javascript
const action = actions.titleActions({ title: 'text' });
```
With payload:

```javascript
{
  type: types.POST_TITLE,
  payload: {
    title: 'text',
  },
}
```

With **asParams** option you can get the same output like with native redux action creator:

```javascript
rl.addAction('title', { title: '' }, { asParams: 'title' });
const { actions } = rl.flush();
```
And you will have action:

```javascript
const action = actions.titleActions('text');
```
With payload:

```javascript
{
  type: types.POST_TITLE,
  title: 'text',
}
```

The same result you can get using addFormElementAction:

```javascript
rl.addParamAction('title', '');
```

**You can put many parameters**:

```javascript
rl.addAction('clear', { title: '', body: '' }, { asParams: ['title', 'body'] });
const { actions } = rl.flush();
```
And you will have action:

```javascript
const action = actions.clearActions('title', 'body');
```
With payload:

```javascript
{
  type: types.POST_TITLE,
  title: 'title',
  body: 'body',
}
```
Or with default data:

```javascript
const action = actions.clearActions();
```
With payload:

```javascript
{
  type: types.POST_TITLE,
  title: '',
  body: '',
}
```

The same result you can get using addFormElementAction:

```javascript
rl.addParamsAction('clear', { title: '', body: '' });
```

## asParams with isFormElement

You can use **asParams** option with **isFormElement**:

```javascript
rl.addAction('title', { title: '' }, { isFormElement: true, asParams: 'title' });
```
And put as props:

```html
<input
  type="text"
  onChange={props.titleAction}
  value={props.title}
/>
```
It returns:

```javascript
{
  type: types.POST_TITLE,
  title: 'Text input data',
}
```

The same result you can get using addFormElementAction:

```javascript
rl.addFormElementAction('title', '');
```

## isReset

To reset you state to default you need to set isReset option

```javascript
rl.addAction('reset', {}, { isReset: true });
```
The same result you can get using addResetAction:

```javascript
rl.addResetAction();
```

If you need to rename you action you can set name:

```javascript
rl.addResetAction('clear');
```

And run it in your code as:

```javascript
clearAction();
```

If you set up default state with actions, state will be merged:

```javascript
const rl = new RL('post', { test: true });

rl.addParamAction(title, 'title');
```

resetAction will return:

```javascript
{ test: true, title: 'title' }
```

To return exactly the same state use exactly option:

```javascript
const rl = new RL('post', { test: true });

rl.addParamAction(title, 'title');
rl.addResetAction('clear', true);
```

clearAction will return:

```javascript
{ test: true }
```

## Documentation

 * [Install](https://github.com/evheniy/redux-lazy/blob/master/docs/install.md)
 * [How to use](https://github.com/evheniy/redux-lazy/blob/master/docs/use.md)
 * [Types](https://github.com/evheniy/redux-lazy/blob/master/docs/types.md)
 * [Actions](https://github.com/evheniy/redux-lazy/blob/master/docs/actions.md)
 * [Reducer](https://github.com/evheniy/redux-lazy/blob/master/docs/reducer.md)
 * [Container](https://github.com/evheniy/redux-lazy/blob/master/docs/container.md)

[More examples](https://github.com/evheniy/redux-lazy/blob/master/tests/actions.js)
