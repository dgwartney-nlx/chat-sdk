# Chat Widget

The chat widget is a styled, configurable UI widget you can drop in on your website or web application.

## Installation

`npm install --save @nlxchat/widget react react-dom`

## Usage

You can render a chat widget in your document with just a few lines of code:

```jsx
import { standalone } from "@nlxchat/widget";

// This will render the widget as the last element in the <body>

standalone({
  config: {
    botUrl: "",
    headers: {
      "nlx-api-key": ""
    },
    triggerWelcomeIntent: true
  },
  initiallyExpanded: true,
  theme: {
    primaryColor: "teal",
    darkMessageColor: "#000",
    lightMessageColor: "#fff",
    fontFamily: "Helvetica"
  }
});
```

If you are running a React application, you can use the component version with the same configuration API as props:

```jsx
import { Widget } from "@nlxchat/widget";

render(<Widget config={{ botUrl: "" }} />, document.getElementById("app"));
```

There is also a packaged version of the SDK that exposes the `chat.standalone` and `chat.widget` as a global on window:

```html
<body>
  <script src="https://unpkg.com/@nlxchat/widget@0.5.0/lib/umd/widget.js"></script>
  <script>
    window.chat.standalone({
      config: {
        botUrl: "",
        headers: {
          "nlx-api-key": ""
        }
      },
      initiallyExpanded: true,
      theme: {
        primaryColor: "teal",
        darkMessageColor: "#000",
        lightMessageColor: "#fff",
        fontFamily: "Helvetica"
      }
    });
  </script>
</body>
```

## Configuration

Initiating the chat takes the following parameters (see [type definition](https://github.com/nlxai/chat-sdk/blob/master/packages/widget/src/props.ts) for details):

### `config`

The configuration of the chat itself, containing `botUrl` and request headers.

### `theme`

Overrides for the visual theme constants. See [Theme type definition](https://github.com/nlxai/chat-sdk/blob/master/packages/widget/src/theme.ts) for details.

### `chatIcon`

The URL of an image you can set to override the default chat icon in the chat pin in the lower right corner. PNG and SVG work best.

### `titleBar`

Renders an optional title bar at the top. If the object is provided, it has the following fields:
* `title` (mandatory): title text.
* `icon` (optional): a URL for an icon image.
* `downloadable` (optional): if set to true, the title bar will include a button that allows chat history to be downloaded.

### `bubble`

When set to a non-empty string, a small bubble will appear above the chat pin when the chat is not expanded, helping the user understand what the chat is for. This bubble appears 3s after the chat is loaded, and disappears after 20s.

### `initiallyExpanded`

Sets whether the widget is initially expanded.

### `lowLevel`

If you need low-level control of the widget, this configuration value gives access to the [conversationHandler](https://github.com/nlxai/chat-sdk/blob/94d5fade43c6ed05ddf95de7140bf5bf1e6f916e/packages/core/src/index.ts#L84-L95) object through a callback, called once on widget initialization:

```jsx
<Widget
  config={{
    botUrl: ""
  }}
  lowLevel={(conversationHandler) => {
    // Send e.g. custom slot values, or save the handler in a ref or on the window global
    conversationHandler.sendSlots([
      {
        slotId: "name",
        value: "Alex"
      }
    ]);
  }
/>
```

## License

MIT.
