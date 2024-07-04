# Popin Integration Document

**POPIN VIDEO SHOPPING**

## Abstract

This document establishes the integration steps to enable popin video shopping on an ecommerce website.

---

## Brand Panel

Your brand panel is available at [https://dashboard.popin.to](https://dashboard.popin.to). You can login using the credentials provided to you.

---

## Installation

Copy the Popin code from your Brand Panel > Settings > Integrations and embed it on all pages on your website from where you'd like your customers to initiate calls with your agents.

The code will look something like this:

```html
<script>
let popIn = document.createElement('script')
popIn.setAttribute('src', 'https://widget01.popin.to/js/widget.js')
document.body.appendChild(popIn)
popIn.onload = () => {
  popInWidgetInit({
    token: "123456",
    mode: "hidden", //optional to hide widget icon
    captured: {     //optional for logged in user
      name: "John Doe",
      mobile: "9876543210",
      email: "john@lorem.com"
    }
  });
}
</script>
```

---

## API Methods

### Record Sale

Use this API to record sale so that it gets attributed to agent.

```javascript
Popin('sale', { orderId, amount })
```

**Parameters**

| Option   | Optional? | Default value | Description                           |
|----------|-----------|---------------|---------------------------------------|
| orderId  | No        |               | OrderId of the sale for internal tracking. |
| amount   | No        |               | Total amount in the transaction in paise.   |

**Example Code**

```javascript
Popin('sale', { orderId: 777, amount: 9000 })
```

---

### Connection Routing

Use this API to route connection to a particular group.

```javascript
Popin('group', { groupId: <id_of_group> })
```

OR use the below code as part of your widget open script.

```html
<button onclick="Popin('open', { groupId: '<id_of_group>' })">Button</button>
```

**Parameters**

| Option   | Optional? | Default value | Description                  |
|----------|-----------|---------------|------------------------------|
| groupId  | No        |               | ID of the group to route call to. |

**Example Code**

```javascript
Popin('group', { groupId: 4 })
```

---

### Open Widget

Use this API to open the widget.

```javascript
Popin('open', { groupId: <id_of_group> })
```

**Parameters**

| Option   | Optional? | Default value | Description                  |
|----------|-----------|---------------|------------------------------|
| groupId  | Yes       |               | ID of the group to route connection to. |

**Example Code**

```javascript
Popin('open', { groupId: 4 })
```

---

### Close Widget

Use this API to close the widget.

```javascript
Popin('close')
```

---

### Sync Products

Use this API to sync product info with popin system so that agents can share products from their devices.

**POST:** [https://widget01.popin.to/api/v1/products](https://widget01.popin.to/api/v1/products)

**Parameters**

```json
{
  "token": "51",
  "products": [
    {
      "name": "Cool Bangle",
      "url": "https://mysite.com/product/cool-bangle",
      "price": 4500,
      "image": "https://mysite.com/images/cool-bangle.jpg"
    },
    {
      "name": "Cool Ring",
      "url": "https://mysite.com/product/cool-ring",
      "price": 1500,
      "image": "https://mysite.com/images/cool-ring.jpg"
    }
  ]
}
```

**Description**

A POST request has to be sent with your token and products info as JSON to the above URL. Please make sure you set the Content-Type header as `application/json`. 

*Note: The amount field is in paise.*

---

## Questions?

Write a mail to [support@popin.to](mailto:support@popin.to)


