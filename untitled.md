# Regression Tests Protocol

### 

[1. Order creation/receiving:]()

[1.1 Create order using kitchen app.]()

[1.2 Create order using GrubHub]()

[1.3 Create order using Deliverect]()

[2. Kitchen App interface]()

[2.1 Order statuses]()

[2.1.1 Start Order]()

[2.1.2 Cancel Order]()

[2.1.3 Skip New Order]()

[2.1.4 Skip Started Order]()

[2.2 Order Items Packaging]()

[2.2.1 Order Item mark as packed \(check with reload\)]()

[2.2.2 Order Item mark as unpacked \(check with reload\)]()

[2.3 Courier dispatching]()

[2.3.1 Automatical courier dispatching]()

[2.3.2 Manual courier dispatching]()

[2.3.3 Courier dispatching functionality displaying]()

[2.4 Orders history]()

[2.4.1 Check if the history represents database data.]()

[3. MIQA Interface]()

[3.1 Orders receiving]()

[3.2 Orders displaying]()

[3.3 Order Item Processing]()

[3.4 Sequence of the order Items displaying]()

## 1. Order creation/receiving:

Pass Criteria 1A. Order creation/receiving pass criteria:

1. Order received through the WebSocket and displayed in the “New” tab on the main page;
2. The order still displayed on the “New” tab after reload;
3. After a minute and a half after the order received - it’s still displayed on the “New” tab;

### 1.1 Create order using kitchen app.

STR: Go to the /testing-orders page and create a new order

Pass criteria: 1A

### 1.2 Create order using GrubHub

Pass criteria: 1A

### 1.3 Create order using Deliverect

Pass criteria: 1A

## 2. Kitchen App interface

 Prerequisites:

1. responsible employees should be selected.

### 2.1 Order statuses

#### 2.1.1 Start Order

STR: Click “Start”

Pass criteria:

1. Order is displayed on both: “New” and “In progress” tabs
2. Order Details Card contains the button “Cancel Start”.

####  2.1.2 Cancel Order

 STR: When the order started - click the “Cancel Start” button

Pass criteria:

1.  Order is displayed only on the “New” tab
2. The “Cancel Start” button is not visible
3. The “Start” button is visible

####  2.1.3 Skip New Order

####  2.1.4 Skip Started Order

 2.1.5 Start Order after login

 STR: Logout - Login - click the “Cancel Start” button

###  2.2 Order Items Packaging

####  2.2.1 Order Item mark as packed \(check with reload\)

####  2.2.2 Order Item mark as unpacked \(check with reload\)

###  2.3 Courier dispatching

 Prerequisites:

1. Received UberEats or Grubhub order, where customer\_location and customer\_name property is not equal to null;

####  2.3.1 Schedule immediate courier dispatching for UberEats order

 STR: Trigger relay courier dispatching for UberEats with delay 0 minutes

 Pass criteria:

1. Received the successful response on the schedule action.
2. Received the successful response on the dispatch action \(in case of error - displayed respective info, otherwise - display successful dispatching status\).
3. Order is visible in the relay dashboard.

#### 2.3.2 Schedule immediate courier dispatching for Grubhub order

 STR: Trigger relay courier dispatching for Grubhub with delay 0 minutes

 Pass criteria:

1. Received the successful response on the schedule action.
2. Received the successful response on the dispatch action \(in case of error - display respective info, otherwise - display successful dispatching status\).
3. Order is visible in the relay dashboard.
4. Check in DB table relay\_order if order\_key contains not order\_id, but ordering\_platform\_original\_id

####  2.3.3 Schedule courier dispatching with timeout and cancellation

STR: Trigger relay courier with delay greater than 0 minutes

 Pass criteria:

1. Received the successful response on the dispatch action \(displayed notification\).
2. Order is visible in the relay dashboard.
3. In cloud task menu - u can see scheduled task with name that equal to stored task\_name for this order in DB.
4. Cancel scheduled courier dispatching using Kitchen App UI
5. Check that cloud task disappeared.
6. Schedule courier dispatching again
7. Received the successful response on the dispatch action \(in case of error - display respective info, otherwise - display successful dispatching status\).

#### 2.3.4 Courier dispatching functionality displaying

 Pass criteria:

1. Dispatch courier button displayed only for not finished order \(neither skipped nor RTD\)

###  2.4 Orders history

 Prerequisites:

1. Open the ‘Orders History’ page.

#### 2.4.1 Check if the history represents database data.

STR:

1. Select a particular date using the calendar \(not today\). Open Network console and find the latest query that has similar URL: /api/v1/orders?startDatetime=2021-01-24T22:00:00.422Z&endDatetime=2021-01-25T21:59:59.422Z
2. Fill in the query below and execute it in MySql Client.

Select id, customer\_fullname, placed\_time

from \`order\`

WHERE \(

 \(

 ${startDate} &lt;= placed\_time AND ${endDate} &gt;= placed\_time

 \)

 OR

 \(

 ${startDate} &lt;= delivery\_time AND ${endDate}&gt;= delivery\_time

 \)

\)

AND kitchen\_id = ‘${kitchen\_Id}’

Pass criteria:

1. The number of orders that satisfy the date parameters is equal in DB and on the display.

 2.5 Responsible employees selection

 2.5.1

##  3. MIQA Interface

###  3.1 Orders receiving

 STR:

1. Click the “Start” order button in the Kitchen App.

 Pass criteria:

1. The order should immediately appear in the MIQA client.
2. If there were no order details card opened - the order details card for the started order should appear on the screen, otherwise - the order should just appear in the orders list without closing the opened card.

###  3.2 Orders displaying

 STR:

1. Open order details card in MIQA interface

 Pass criteria:

1. Order details card contains only order items list with the single allowed actions: check the item \(including the results menu\) and see the photo of the item \(if the photo exists\)
2. Displayed only orders which have ‘inProgress’ preparation status

### 3.3 Order Item Processing

1. The system provides feedback about the specific product on the display of the MIQA and by making a proper sound.
   1. If everything is good - the hub employee doesn’t have to do anything, the system will finalize the product automatically after a certain timeout \(30 seconds?\)
   2. If the system recognized the product does not meet the standard - the employee can trigger a “recheck” that will initiate the same process again OR he can manually “Finalize” the product despite system warning.
      1. If the employee manually finalizes the product - he can choose a reason out of a list of reasons:
         1. Not specified \(default\)
         2. Wrong measurement \(the product is good\)
         3. Missing product information \(the system doesn’t know how to check\)
         4. Customer notes \(the customer asked for something that cannot be automatically checked\)
      2. If the employee does nothing within 30 seconds - the product is automatically Finalized with a reason “Automatic”. The employee can stop the timer of 30 seconds by clicking “Stop the countdown”.
   3. If for any reason the product was not correctly recognized - the hub employee can select a different product from the list of order products or even chose a different order if there is more than one order in process. The employee can change the order and the product at any time, regardless of the results of the current check.
      1. Whenever a different product is selected - it is checked without retaking new measurements. The old measurements are compared to the new product’s standard.

###  3.4 Sequence of the order Items displaying

 Pass criteria:

1. Products that require QA are shown first.
2. The same products are shown in succession \(in a row\).

