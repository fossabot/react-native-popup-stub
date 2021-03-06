# react-native-popup-stub

[![Open Source Love](https://badges.frapsoft.com/os/mit/mit.svg?v=102)](https://github.com/ellerbrock/open-source-badge/)
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)
  
## Introduction 
Popup global controller:

- Handles popup animations
- Remove old popup that has the same zIndex automatically

Derived from @unpourtous/react-native-stub-toast/PopupStub.

Animation is based on [react-native-animatable](https://github.com/oblador/react-native-animatable)

## Installation 
```
npm install @unpourtous/react-native-popup-stub --save
```

## Usage
First, add PopupStub as sibling node of you Root Node
``` js
export default class example extends Component {
  render () {
    return (
      <View style={styles.container}>
        {/* Your root node */} 
        <TouchableHighlight
          onPress={() => {
            // Step three: Use Toast with static function
            Toast.show('This is a Toast')
            Toast.show('This is another Toast')
          }}>
          <Text>Show Toast</Text>
        </TouchableHighlight>
        
        {/* Step One: Add popup stub */} 
        <PopupStub ref={_ref => {
          // Step Two: Init PopupStub itself
          PopupStub.init(_ref)
        }} />
      </View>
    )
  }
}
```

Then, just push your popup instance to PopupStub
```js
export default class Toast extends Component {
  static show (msg) {
    const id = PopupStub.stub.addPopup(<Toast msg={msg} />, {
      mask: false,
      position: 'center',
      zIndex: 500,
      delay: 0,
      duration: 100,
      animation: 'fadeIn',
      easing: 'ease'
    })
    // autoclose after 1.5s
    setTimeout(() => {
      PopupStub.stub.removePopup(id)
    }, 1500)
  }
  
  render () {
    return (
      <View style={{alignSelf:'center'}}>
        <Text>{this.props.msg}</Text>
      </View>
    )
  }
}
```

## License
This library is distributed under MIT Licence.


[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bhttps%3A%2F%2Fgithub.com%2FUnPourTous%2Freact-native-popup-stub.svg?type=large)](https://app.fossa.io/projects/git%2Bhttps%3A%2F%2Fgithub.com%2FUnPourTous%2Freact-native-popup-stub?ref=badge_large)