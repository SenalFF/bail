l

Install in package.json:
```json
"dependencies": {
    "baileys": "github:nstar-y/bail"
}
```
or install in terminal:
```
npm install baileys@github:nstar-y/bail
```

Then import the default function in your code:
```ts 
// type esm
import makeWASocket from 'baileys'
```

```js
// type cjs
const { default: makeWASocket } = require("baileys")
```

## Added Features and Improvements

| Feature                               | Description                                                                                                                               |
| :------------------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------- |
| 💬 **Send Messages to Channels**     | Supports sending text and media messages to channels.                                                                                     |
| 🔘 **Button & Interactive Messages** | Supports sending button messages and interactive messages on WhatsApp Messenger and WhatsApp Business.                                   |
| 🖼️ **Send Album Messages**           | Supports sending multiple images as an album (grouped media message), enabling richer and more organized media sharing.                  |
| 👥 **Group with LID Support**       | Full support for group using `@lid`, ensuring compatibility with the latest WhatsApp group addressing format.                         |
| 🤖 **AI Message Icon**               | Customize message appearances with an optional AI icon, adding a modern touch.                                                            |
| 🖼️ **Full-Size Profile Pictures**    | Allows users to upload profile pictures in their original size without cropping, ensuring better quality and visual presentation.         |
| 🔑 **Custom Pairing Codes**          | Users can now create and customize pairing codes as they wish, enhancing convenience and security when connecting devices.                |
| 🛠️ **Libsignal Fixes**               | Enjoy a cleaner development experience with refined logs, providing more informative and less cluttered output from the libsignal library.|

More features and improvements will be added in the future.

## Feature Examples

Here are some examples of features that have been added:

### Newsletter Management

- **To get info newsletter**

const metadata = await sock.newsletterMetadata("invite", "xxxxx")
// or
const metadata = await sock.newsletterMetadata("jid", "abcd@newsletter")
console.log(metadata)

- **To update the description of a newsletter**

await sock.newsletterUpdateDescription("abcd@newsletter", "New Description")

- **To update the name of a newsletter**

await sock.newsletterUpdateName("abcd@newsletter", "New Name")

- **To update the profile picture of a newsletter**

await sock.newsletterUpdatePicture("abcd@newsletter", buffer)
- **To remove the profile picture of a newsletter**

await sock.newsletterRemovePicture("abcd@newsletter")

- **To mute notifications for a newsletter**

await sock.newsletterUnmute("abcd@newsletter")

- **To mute notifications for a newsletter**

await sock.newsletterMute("abcd@newsletter")

- **To create a newsletter**

const metadata = await sock.newsletterCreate("Newsletter Name")
console.log(metadata)

- **To delete a newsletter**

await sock.newsletterDelete("abcd@newsletter")

- **To follow a newsletter**

await sock.newsletterFollow("abcd@newsletter")

- **To unfollow a newsletter**
await sock.newsletterUnfollow("abcd@newsletter")

- **To send reaction**

// jid, id message & emoticon
// way to get the ID is to copy the message url from channel
// Example: [ https://whatsapp.com/channel/xxxxx/175 ]
// The last number of the URL is the ID
const id = "175"
await sock.newsletterReactMessage("abcd@newsletter", id, "🥳")


### Button and Interactive Message Management

- **To send button with text**

const buttons = [
  { buttonId: 'id1', buttonText: { displayText: 'Button 1' }, type: 1 },
  { buttonId: 'id2', buttonText: { displayText: 'Button 2' }, type: 1 }
]

const buttonMessage = {
    text: "Hi it's button message",
    footer: 'Hello World',
    buttons,
    headerType: 1
}

await sock.sendMessage(id, buttonMessage, { quoted: null })

- **To send button with image**

const buttons = [
  { buttonId: 'id1', buttonText: { displayText: 'Button 1' }, type: 1 },
  { buttonId: 'id2', buttonText: { displayText: 'Button 2' }, type: 1 }
]

const buttonMessage = {
    image: { url: "https://example.com/abcd.jpg" }, // image: buffer or path
    caption: "Hi it's button message with image",
    footer: 'Hello World',
    buttons,
    headerType: 1
}

await sock.sendMessage(id, buttonMessage, { quoted: null })


- **To send button with video**

const buttons = [
  { buttonId: 'id1', buttonText: { displayText: 'Button 1' }, type: 1 },
  { buttonId: 'id2', buttonText: { displayText: 'Button 2' }, type: 1 }
]

const buttonMessage = {
    video: { url: "https://example.com/abcd.mp4" }, // video: buffer or path
    caption: "Hi it's button message with video",
    footer: 'Hello World',
    buttons,
    headerType: 1
}

await sock.sendMessage(id, buttonMessage, { quoted: null })


- **To send interactive message**

const interactiveButtons = [
     {
        name: "quick_reply",
        buttonParamsJson: JSON.stringify({
             display_text: "Quick Reply",
             id: "ID"
        })
     },
     {
        name: "cta_url",
        buttonParamsJson: JSON.stringify({
             display_text: "Tap Here!",
             url: "https://www.example.com/"
        })
     },
     {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
             display_text: "Copy Code",
             id: "12345",
             copy_code: "12345"
        })
     }
]

const interactiveMessage = {
    text: "Hello World!",
    title: "this is the title",
    footer: "this is the footer",
    interactiveButtons
}

await sock.sendMessage(id, interactiveMessage, { quoted: null })

- **To send interactive message with image**

const interactiveButtons = [
     {
        name: "quick_reply",
        buttonParamsJson: JSON.stringify({
             display_text: "Quick Reply",
             id: "ID"
        })
     },
     {
        name: "cta_url",
        buttonParamsJson: JSON.stringify({
             display_text: "Tap Here!",
             url: "https://www.example.com/"
        })
     },
     {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
             display_text: "Copy Code",
             id: "12345",
             copy_code: "12345"
        })
     }
]

const interactiveMessage = {
    image: { url: "https://example.com/abcd.jpg" }, // image: buffer or path
    caption: "this is the caption",
    title: "this is the title",
    footer: "this is the footer",
    interactiveButtons
}

await sock.sendMessage(id, interactiveMessage, { quoted: null })

- **To send interactive message with video**

const interactiveButtons = [
     {
        name: "quick_reply",
        buttonParamsJson: JSON.stringify({
             display_text: "Quick Reply",
             id: "ID"
        })
     },
     {
        name: "cta_url",
        buttonParamsJson: JSON.stringify({
             display_text: "Tap Here!",
             url: "https://www.example.com/"
        })
     },
     {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
             display_text: "Copy Code",
             id: "12345",
             copy_code: "12345"
        })
     }
]

const interactiveMessage = {
    video: { url: "https://example.com/abcd.mp4" }, // video: buffer or path
    caption: "this is the caption",
    title: "this is the title",
    footer: "this is the footer",
    interactiveButtons
}

await sock.sendMessage(id, interactiveMessage, { quoted: null })

- **To send list interactive**

const interactiveButtons = [
  {
    name: "single_select",
    buttonParamsJson: JSON.stringify({
      title: "message",
      sections: [
        {
          title: "title",
          highlight_label: "label",
          rows: [
            {
              header: "HEADER",
              title: "TITLE",
              description: "DESCRIPTION",
              id: "YOUR ID"
            },
            {
              header: "HEADER",
              title: "TITLE",
              description: "DESCRIPTION",
              id: "YOUR ID"
            }
          ]
        }
      ]
    })
  }
];

const interactiveMessage = {
    text: "Hello World!",
    title: "this is the title",
    footer: "this is the footer",
    interactiveButtons
};

await sock.sendMessage(id, interactiveMessage, { quoted: null })

### Send Album Message

// Media can be a URL, buffer, or path.
const media = [
  {
    image: { url: "https://example.com/image.jpg" }
  },
  {
    image: await getBuffer("https://example.com/image.jpg")
  },
  {
    video: { url: "https://example.com/video.mp4" }
  }
]

await sock.sendMessage(id, { album: media, caption: "testing send album" }, { quoted: null })


### AI Message Icon Customization


// To enable the AI icon for a message, simply add the "ai: true" parameter:
await sock.sendMessage(id, { text: "Hello World", ai: true });


### Custom Pairing Code Generation

if(usePairingCode && !sock.authState.creds.registered) {
    const phoneNumber = await question('Please enter your mobile phone number:\n');
    // Define your custom 8-digit code (alphanumeric)
    const customPairingCode = "NSTRCODE";
    const code = await sock.requestPairingCode(phoneNumber, customPairingCode);
    console.log(`Your Pairing Code: ${code?.match(/.{1,4}/g)?.join('-') || code}`);
}
