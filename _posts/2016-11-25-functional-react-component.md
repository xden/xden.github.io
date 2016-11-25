---
published: true
title: Functionally Composed React Component
---
old code
```javascript 
import React from 'react';
import Paper from 'material-ui/Paper';

import CloseButton from '../internal/CloseButton';
import ButtonEdit from '../ButtonEdit.js';


export default class Element extends React.Component {
  state = {
    closeButtonShown: false,
    editButtonShown: false,
  };

  handleMouseEnter = (event) => {
    // do not react when add button is entered
    if (!event.target.classList.contains('add')) {
      this.setState({
        closeButtonShown: true,
        editButtonShown: true,
      });
    }
    if (this.props.onMouseEnter) this.props.onMouseEnter(event);
  };

  handleMouseLeave = (event) => {
    this.setState({
      closeButtonShown: false,
      editButtonShown: false,
    });
    if (this.props.onMouseLeave) this.props.onMouseLeave(event);
  };

  render() {
    const { style, children, id, removeHandler, ...otherProps } = this.props;

    const combinedStyle = {
      border: '1px solid',
      display: 'inline-block',
      padding: '1em',
      marginBottom: '80px',
      position: 'relative',
      backgroundColor: this.state.editButtonShown && 'rgba(0,0,0,0.078)',
      ...style,
    };

    return (
      <Paper
        id={id}
        style={combinedStyle}
        onMouseLeave={this.handleMouseLeave}
        onMouseEnter={this.handleMouseEnter}
        {...otherProps}
      >
        <ButtonEdit
          dataId={id}
          style={{
            opacity: this.state.editButtonShown ? 1 : 0,
          }}
        />
        {
          removeHandler ?
            <CloseButton
              style={{
                opacity: this.state.closeButtonShown ? 1 : 0,
              }}
              onTouchTap={removeHandler}
            /> : null
        }
        {children}
      </Paper>
    );
  }
}
```

New code with recompose
```javascript
import React from 'react';
import Paper from 'material-ui/Paper';
import fp from 'lodash/fp';

import CloseButton from '../internal/CloseButton';
import ButtonEdit from '../ButtonEdit.js';

import {
  compose,
  mapProps,
  withHandlers,
  withProps,
  withState,
} from 'recompose'

const enhance = compose(
  withState('closeButtonShown', 'setCloseButtonShown', false),
  withState('editButtonShown', 'setEditButtonShown', false),
  withHandlers({
    handleMouseLeave: props => event => { // eslint-disable-line
      props.setCloseButtonShown(false);
      props.setEditButtonShown(false);
    },
    handleMouseEnter: props => evnt => { // eslint-disable-line
      props.setCloseButtonShown(true);
      props.setEditButtonShown(true);
    }
  }),
  withProps(({ style, editButtonShown }) => ({
    combinedStyle: {
      border: '1px solid',
      display: 'inline-block',
      padding: '1em',
      marginBottom: '80px',
      position: 'relative',
      backgroundColor: editButtonShown && 'rgba(0,0,0,0.078)',
      ...style,
    },
  })),
  mapProps(fp.omit([
    'setCloseButtonShown',
    'setEditButtonShown',
    'style'
  ])),
)

export default enhance(({
  children,
  closeButtonShown,
  combinedStyle,
  editButtonShown,
  handleMouseEnter,
  handleMouseLeave,
  id,
  removeHandler,
  ...otherProps
}) => (
  <Paper
    id={id}
    style={combinedStyle}
    onMouseLeave={handleMouseLeave}
    onMouseEnter={handleMouseEnter}
    {...otherProps}
  >
    <ButtonEdit
      dataId={id}
      style={{
        opacity: editButtonShown ? 1 : 0,
      }}
    />
    {
      removeHandler ?
        <CloseButton
          style={{
            opacity: closeButtonShown ? 1 : 0,
          }}
          onTouchTap={removeHandler}
        /> : null
    }
    {children}
  </Paper>
));

```
