# front-sdk
An SDK for working with Front (https://frontapp.com).

## TypeScript Quickstart

Import in the usual way:

```typescript
import { Front } from 'front-sdk';
```

## JavaScript

Require in the usual way:

```javascript
const Front = require('front-sdk').Front;
```

## Usage

Create a new instance of the SDK to use it, passing the API token for Front.

```typescript
import { Comment, Front } from 'front-sdk';
const front = new Front('abcdef123457890');

front.comment.create({
    conversation_id: 'cnv_xxxx',
    author_id: `alt:email:back@tofront`,
    body: 'It is very important that you see this comment!'
}).then((comment: Comment) => {
    console.log(comment);
}).catch(FrontError, (err: FrontError) => {
    console.log(err);
});
```

Can also be used as a callback, if required:

```typescript
front.comment.create({
    conversation_id: 'cnv_xxxx',
    author_id: `alt:email:back@tofront`,
    body: 'It is very important that you see this comment!'
}, (err: FrontError, comment: FrontComment) => {
    if (err) {
        console.log(err);
        return;
    }

    console.log(comment);
});
```

#### Notes

To post into a Front Inbox, you need to know the correct channels in for it.
Channels are instances of sources, such as SMTP, Facebook, Front Integrations, etc.

So to post a new Conversation:
 * Find the Inbox required want
 * List the Channels and find the correct one for the source (Integration channels, in the SDK case)
 * Post a Message to that Channel (which will return a Conversation reference)

To post a Comment or Message to that Conversation:
 * Use the Conversation reference to post (returns a Comment or Message object)
