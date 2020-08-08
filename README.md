# twilio-react-chat-window

`twilio-react-chat-window` provides an intercom-like chat window that can be included easily in any project and integrated into Twilio. It provides no messaging facilities, only the view components.

Based on react-chat-window from https://github.com/kingofthestack/react-chat-window

![Demo gif of react-chat-window being used](https://puu.sh/xei2F/fd4a121185.gif)

## [Demo](https://kingofthestack.github.io/react-chat-window/)

## Table of Contents
- [Installation](#installation)
- [Example](#example)
- [Components](#components)

## Installation

```
$ npm install react-chat-window
```

## Example

``` javascript
import React, {Component} from 'react'
import {Launcher} from 'react-chat-window'

class Demo extends Component {

  constructor() {
    super();
    this.state = {
      messageList: []
    };
  }

  _onMessageWasSent(message) {
    this.setState({
      messageList: [...this.state.messageList, message]
    })
  }

  _sendMessage(text) {
    if (text.length > 0) {
      this.setState({
        messageList: [...this.state.messageList, {
          author: 'them',
          type: 'text',
          data: { text }
        }]
      })
    }
  }

  render() {
    return (<div>
      <Launcher
        agentProfile={{
          teamName: 'react-chat-window',
          imageUrl: 'https://a.slack-edge.com/66f9/img/avatars-teams/ava_0001-34.png'
        }}
        // messageComponent={(props) => <p>{props.message.data.text}</p>}
        // headerComponent={<div>header</div>}
        onMessageWasSent={this._onMessageWasSent.bind(this)}
        messageList={this.state.messageList}
        showEmoji
      />
    </div>)
  }
}
```

For more detailed examples see the demo folder.

## Components

# Launcher

`Launcher` is the only component needed to use react-chat-window. It will react dynamically to changes in messages. All new messages must be added via a change in props as shown in the example.

Launcher props:

|      prop        | type   | required | description |
|------------------|--------|----------|-------------|
| agentProfile     | [object](#agent-profile-objects) | yes | Represents your product or service's customer service agent. Fields: imageUrl (string), teamName (string). |
| handleClick      | function | yes | Intercept the click event on the launcher. No argument sent when function is called. |
| isOpen           | boolean | yes | Force the open/close state of the chat window. If this is not set, it will open and close when clicked. |
| messageList      | [[message](#message-objects)] | yes | An array of message objects to be rendered as a conversation. |
| mute             | boolean | no | Don't play sound for incoming messages. Defaults to `false`. |
| newMessagesCount | number | no | The number of new messages. If greater than 0, this number will be displayed in a badge on the launcher. Defaults to `0`. |
| onFilesSelected  | function([fileList](https://developer.mozilla.org/en-US/docs/Web/API/FileList)) | no | Called after file has been selected from dialogue in chat window. |
| onMessageWasSent | function([message](#message-objects)) | yes | Called when a message is sent, with a message object as an argument. |
| showEmoji        | boolean | no | Whether or not to show the emoji button in the input bar. Defaults to `true`.
| userInputComponent | react node | no | Replace the user input component.
| headerComponent | react node | no | Replace the header component.
| messageComponent | react component | no | Replace the message component, make sure this component has "message" props(a message is an object)


### Message Objects

Message objects are rendered differently depending on their type. Currently, only text, file, and emoji types are supported. Each message object has an `author` field which can have the value 'me' or 'them'.

``` javascript
{
  author: 'them',
  type: 'text',
  data: {
    text: 'some text'
  }
}

{
  author: 'me',
  type: 'emoji',
  data: {
    code: 'someCode'
  }
}


{
  author: 'me',
  type: 'file',
  data: {
    url: 'somefile.mp3',
    fileName: 'Any old name'
  }
}

```

### Agent Profile Objects

Look like this:

```js
{
  imageUrl: 'https://somewhere.on/the_web.png',
  teamName: 'Da best'
}
```

## Building

Run `npm run build` before publishing to create ES and UMD modules.
