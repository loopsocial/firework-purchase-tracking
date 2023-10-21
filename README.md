
![ezgif com-webp-to-png](https://github.com/fireworkads/Firework-Tag-Template/assets/87154260/19af597b-b44b-437c-9a11-f4b666c362ea)


# Firework Purchase Tracking

## Introdution

Firework Purchase Tracking gives you valuable insights for user's shopping experience and performance when buying products in your website. The Firework Purchase Tracker enables merchants to capture relevant sales related actions from customers that have interacted with Firework player. 

By implementing the **Firework Purchase Tracking tag**, we can determine the GMV and AOV attributed to Firework. 

## Implementation

You can add the Firework Purchase Tracking Tag to your 'Purchase Confirmation' in different ways:
1. Add it directly to your application code, you'll need to follow our [general implementation guide](https://docs.firework.com/home/web/integration-guide/shopping-integration-v2/tracking).
2. Or inject it through a tag manager solution such as Google Tag Manager, Tealium, and Adobe Analytics

This guide is going to cover the implementation using [Google Tag Manager](https://tagmanager.google.com/). The Firework Purchase Tracking tag is designed to capture specific purchase events on your website. In order to ensure accurate data capture, it is essential to correctly configure a new tag using the Firework Purchase Tracking Tag Template and push the necessary information to the Google Tag Manager [dataLayer](https://developers.google.com/tag-platform/tag-manager/datalayer) object on your web pages.

## Requirements
1. Google Tag Manager implemented
2. a datalayer object from Google Tag Manager pushing the order details
   
```javascript
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  order_id: '101045043',
  order_value: 25,
  currency: 'USD',
  subtotal: 0.00,
  shipping_price: 0,
  country: 'USA'
});
</script>
```
3. A Trigger for when an order is completed (purchase confirmation page)


## Implementation Steps
    
1. ###  Add the Firework Purchase Tracking Tag template from within Tag Manager
Our tag is available on Google Tag Manager Community Template Gallery. 

**To search for and add the Firework tag template:**
1. From within Tag Manager, click **Templates**.
2. In the **Tag Templates** section, click **Search Gallery**.
3. To filter the list, click <img width="27" src="https://github.com/fireworkads/Firework-Tag-Template/assets/87154260/3febe355-5c2e-4830-a37d-99a6ab5d34bc"> to open the search field and type "Firework Purchase Tracking" to show the Firework template.
4. Click on the Firework Purchase Tracking Tag template from the result to view details.
5. To add the template, click **Add to workspace**.
6. Review the required template permissions and click **Add**. 

2. ###  Add a new tag using the Firework Purchase Tracking template
In your Workspace, click <img height="20" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/076fc37e-537c-4e46-9854-804c23612921"> Tags.

a. Go to tags and create a new tag from our template (Firework Purchase Tracking). To add a tag, click **New**.
b. Name your tag
   Optional: Add a note to your configuration for later reference. ...
c. Add the triggering   
d. Click **Save** and create more tags as needed.  

<img width="1840" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/e5f29090-b3cb-4219-b19d-60297ac19d3e">

    
### Tag Manager Preview Mode:
Enable the [Preview mode](https://support.google.com/tagmanager/answer/6107056) in Google Tag Manager.
Navigate to the DataLayer tab in the Tag Manager Preview panel.
Verify that the FireWork Purchase Event is visible under the dataLayer section and is not loaded as a variable of type Object. It should be present as a distinct entry within the dataLayer.

### Tag Testing:
Test the implementation by making a test purchase on your website.
Check the Tag Manager Preview panel to ensure that the FireWork Purchase Event is triggered correctly and the data is captured in the dataLayer.

