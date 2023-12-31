<p align="center">
  <a href="https://firework.com" target="_blank" align="center"><img src="https://firework.com/wp-content/uploads/2023/05/Firework-Logo-Black-1.png"></a>
</p>

# Firework Purchase Tracking

## Introdution

**Firework Purchase Tracking** gives you valuable insights for user's shopping experience and performance when buying products in your website. The Firework Purchase Tracker enables merchants to capture relevant sales related actions from customers that have interacted with Firework player. 

By implementing the **Firework Purchase Tracking**, we can determine the **GMV** and **AOV** attributed to Firework. 

You can add the Firework Purchase Tracking Tag in different ways:
  1. Add it directly to your application code - just follow our [general implementation guide](https://docs.firework.com/home/web/integration-guide/shopping-integration-v2/tracking).
  2. Or inject it through a tag manager solution such as Google Tag Manager (GTM), Tealium or Adobe Analytics.
  3. Import our [template file](https://github.com/loopsocial/firework-purchase-tracking/blob/main/template.tpl) into your Google Tag Manager container.

> [!NOTE]
> This guide covers the **Firework Purchase Tracking** implementation using [Google Tag Manager](https://tagmanager.google.com/). The Firework Purchase Tracking tag is designed to capture specific purchase events on your website. In order to ensure accurate data capture, it is essential to correctly configure a new tag using the Firework Purchase Tracking Template and push the necessary information to the Google Tag Manager `dataLayer` object on your web pages.

## Requirements
1. Google Tag Manager [implemented](https://developers.google.com/tag-platform/tag-manager/web)
2. a `datalayer` object from Google Tag Manager pushing the order details, see an example below
   
```JavaScript
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  order_id: '12345',
  order_value: '50.54',
  currency: 'CAD',
  country: 'Canada',
  subtotal: '40.89',
  payment_method: 'AMEX',
  product: [{ ext_product_id: '4483', price: 31, quantity: 15 }],
  ext_customer_identifier: '1234-1234-1234-1234'
});
</script>
```
3. Create new GTM DataLayer [variables](https://support.google.com/tagmanager/answer/6164391?#:~:text=Set%20up%20the%20data%20layer%20variable) based on the data points 

> [!IMPORTANT]
> This implementation requires the following data points to be pushed to the `dataLayer` in order to send properly the purchase information to Firework:
>
>  - `order_id`: string<br/>
>  ID of an order/transaction e.g. '12345'
>
>  - `order_value`: number<br/>
>  total value of the order, e.g. 100
>
>  - `currency`: string<br/>
>  currency in which the order_value was purchased. See a [list](https://en.wikipedia.org/wiki/ISO_4217) of supported currency codes. E.g. 'USD', 'CAD' etc.
>
>  - `country`: string<br/>
>  customer's country 
>  
>  - `subtotal`?: number
>
>  - `payment_method`?: string<br/>
>  order's payment method, e.g.: AMEX, VISA, etc
>
>  - `product`?: Array<{ ext_product_id: string; price: number; quantity: number }><br/>
>  A comma-separated string or an array of product IDs, its prices and quantities that were part of the Order.
>
>  - `ext_customer_identifier`?: string<br/>
>  A way to pass merchants's user ID to its customers

  
  <br/>
  
  More information about the `dataLayer`: https://developers.google.com/tag-platform/tag-manager/datalayer
  
  <br/>
  
4. A [Trigger](https://support.google.com/tagmanager/answer/7679316) for when an order is completed (purchase confirmation page)


## Implementation Steps
    
  1. ###  Add the Firework Purchase Tracking Tag template from within Tag Manager
  Our tag is available on [Google Tag Manager Community Template Gallery](https://tagmanager.google.com/gallery). 

  **To search for and add the Firework tag template:**
  - From within Tag Manager, click **Templates**.
  - In the **Tag Templates** section, click **Search Gallery**.
  - To filter the list, click <img width="32" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/4cab0ae8-9246-4876-b9a6-292ff1f94416"> to open the search field and type "Firework Purchase Tracking" to show the Firework template.
  - Click on the **Firework Purchase Tracking Tag template** from the result to view details.
  - To add the template, click **Add to workspace**.
  - Review the required template permissions and click **Add**. 
  
  2. ### Create new GTM DataLayer [variables](https://support.google.com/tagmanager/answer/6164391?#:~:text=or%20returning%20customer-,Create%20a%20data%20layer%20variable,-Data%20layer%20variables)
  - Click **Variables**.
  - Under **User-Defined Variables**, click **New**.
  - Click **Variable Configuration** and select **Data Layer Variable** as the variable type.

    <img width="2672" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/eb777e2c-51ca-4ff0-b319-1060c3055739">
    
  - In the **Data Layer Variable Name field**, enter the key exactly as it was written in the code (e.g. order_id, not order id.)

  | <img width="2672" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/bba4e3b5-c57a-401a-bc6d-a406e0f31800"> |
  |:--:| 
  | *New DataLayer variable saved* |
    
  - In most cases you should leave the **Data Layer Version** set to the default value of Version 2. Learn more.
  - Save the variable.

  | <img width="2672" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/3d3905ad-6646-4e43-a356-035e380d780d"> |
  |:--:| 
  | *Naming a new dataLayer variable* |
    
  - Repeat these steps for every data layer key that you would like to have available as a variable in Tag Manager.
  
  | <img width="2672" alt="Screenshot 2023-10-27 at 9 28 00 AM" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/6e48b4ff-fd59-46d8-b40c-a62969085e0d"> |
  |:--:| 
  | *New DataLayer variable saved* |
  
  3. ###  Add a new tag using the Firework Purchase Tracking template and assign a trigger
  In your Workspace, click <img height="20" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/076fc37e-537c-4e46-9854-804c23612921"> Tags.

  - Go to tags and create a new tag from our template (Firework Purchase Tracking). To add a tag, click **New**.
  - Associate to each field its corresponding `dataLayer` variable

    

  > Data layer variables enable Google Tag Manager to read values from your data layer implementation and pass those values to tags, triggers, and other variables. A data layer object is made up of a list of key/value pairs.
    
  - **Name** your tag
    Optional: Add a note to your configuration for later reference. ...
  - Add the **triggering**, in our example we have selected to show the new tag on every page which is a default existing trigger in Google Tag Manager. You can also choose to create your own trigger that can be based on many different rules. For example, you could trigger the tag on only certain pages, or after a certain time the user have spent on the page.
    
    <img width="1840" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/87a8a123-eefb-4593-9d2a-9014a96e5804">

    
  - Click **Save**.
  
  4. ### Validate the implementation
  Google Tag Manager has a preview feature that you can now use to test the integration before putting it live on your website.
  
  - Enable the [Preview mode](https://support.google.com/tagmanager/answer/6107056) in Google Tag Manager.

  <img width="2672" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/784bd9d8-183d-42ac-aacd-e9fb993176b4">
    
  - Navigate to the DataLayer tab in the Tag Manager Preview panel.
  - Verify that the FireWork Purchase Event is visible under the `dataLayer` section and is not loaded as a variable of type Object. It should be present as a distinct entry within the `dataLayer`.

  <img width="2672" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/fb007c30-61c3-4907-a852-803b1a347792">

    
  - Test the implementation by making a test purchase on your website.
  - Check the Google Tag Manager Preview panel to ensure that the FireWork Purchase Event is triggered correctly and the data is captured in the `dataLayer`.

  5. ### Publish the new tag
  When your new tag is working as intended, [publish](https://support.google.com/tagmanager/answer/6107163) it.

  To publish your current workspace:
  
  - Click **Submit** at the top right hand side of the screen. The **Submit Changes** screen will appear, with options to publish the container and save a version of your container.
  - Select **Publish and Create Version** if it is not already selected.
  - Review the **Workspace Changes** section to see if your configuration appears as you expect.
  - Enter a **Version Name** and **Version Description**.
  - Click **Publish**.
    <img width="2672" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/a0015b6f-ba52-4e12-8421-eab7039bfa0e">


## Troubleshooting

If you place a test order but cannot see the`dataLayer` section within Google Tag Manager, here's some steps to help you to fix it. 
You will need to use your browser DevTools or any similar tool, such as Charles Proxy for furhter troubleshooting:

1. Confirm if the **Firework Purchase Tracking Library** was loaded from `https://asset.fwcdn3.com/js/analytics.js` on your page, before your purchase script/the GTM tag is fired.
   <img width="1840" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/78f5b334-b499-4de2-9d1c-8ddb5a8802eb">

2. Check the network calls when completing the purchase. There must be a metrics call to `https://p2.fwpixel.com/trk/user:purchase` returning a 200 status. The payload will be similar to:

   ```TopoJSON
   {
     "platform":"web",
     "product":"embed.web.naboo",
     "product_version":"v20231018.1-hotfix",
     "track_version":"2.0",
     "client_event_time":"2023-10-23T10:34:55.090",
     "os_name":"MacOS",
     "event_properties":{
       "locale":"en-US",
       "page_load_id":"90e4c277-5d99-4598-afbd-5371d5d38274",
       "page_url":"https://firework.com/firework-purchase-tracking.html",
       "session_count":39,
       "_last_channel_id":"1ePm6O",
       "_last_video_id":"gd3qDZ",
       "last_engaged_timestamp":"2023-10-17T17:46:28.265Z",
       "user_data":{
         "order_value":"35.54",
         "order_id":"23423",
         "currency":"CAD",
         "subtotal":"31.89",
         "country":"Canada"
       }
     },
     "session_id":"7f8f797a-fd7e-4523-8591-0d7a83081589",
     "session_type":"embed_session",
     "guest_id":"47ef059a-a99d-4d2c-80d1-7cfd5b396803",
     "visitor_id":"47ef059a-a99d-4d2c-80d1-7cfd5b396803"
   }
   ```
  <img width="1840" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/72c981bd-cc6e-4535-8dbc-5843daeb3d32">

   
  <img width="1840" src="https://github.com/loopsocial/firework-purchase-tracking/assets/87154260/551fdf92-f5d3-4e85-8cb7-d0ac2407d035">
