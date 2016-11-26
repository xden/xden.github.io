---
published: true
title: Dividing React Component
---
Writing a program is like drawing. Both start from nothing to a very complex artifact. The reason human being can build those complex artifacts is that a complex artifact can be divided to small pieces. The same goes to writing react component. A react component is usally represented by a class whose structure is not easy to see. An alternative is to compose the component by some utility functions.

<!-- more -->

The same React component in class and functional form are given bellow. The class form uses ES6's class suger syntax, while the functional form uses the Recompose package. 

### Example component in class.

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
  };

  handleMouseLeave = (event) => {
    this.setState({
      closeButtonShown: false,
      editButtonShown: false,
    });
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
         <CloseButton
            style={{
              opacity: this.state.closeButtonShown ? 1 : 0,
            }}
            onTouchTap={removeHandler}
       	  />
        {children}
      </Paper>
    );
  }
}
```

### Example component composed by functions.

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
      <CloseButton
        style={{
          opacity: this.state.closeButtonShown ? 1 : 0,
        }}
        onTouchTap={removeHandler}
      />
    {children}
  </Paper>
));
```

### Comparison

1.

The comparison of these two forms shows that the functional form has better clarity than its opponent.  