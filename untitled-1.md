# System Updates

Candidates:

### Restricted unauthorized access to fileUploader

### Restricted unauthorized access to relayClient

## Version 0.14.0; Release:

DEPLOYMENT SCENARIO

https://docs.google.com/document/d/1O8T7IsbmRf3RjHslVAJmCYVwoUuMAMXnX2KaA8x2Iww/edit

FEATURES:

| User story | Feature short description | Affected Services | Created Services | Tester |
| :--- | :--- | :--- | :--- | :--- |
| https://app.asana.com/0/1176875688547201/1199956448592077 | Kitchen app improvements | Kitchen App |  |  |
| https://app.asana.com/0/1176875688547201/1199919919432624 | Parse Square delivery orders |  | SquareUp parser |  |
| https://app.asana.com/0/1176875688547201/1199904840913868 | Dispatch Relay courier for GH | Relay client, Kitchen Backend |  |  |
| https://app.asana.com/0/1176875688547201/1199634344296623 | Scheduled courier dispatching | Kitchen App, Kitchen Backend |  |  |

MIGRATIONS:

| Story point | Migration name | Affected Storages | Date |
| :--- | :--- | :--- | :--- |
|  | 2020-12-20\(2\)-order-item-status-change-status-column | MySql |  |
|  | 2021-02-01-add-deliverect-channel-link | MySql |  |

## Version 0.10.0; Release:

DEPLOYMENT SCENARIO

[https://docs.google.com/document/d/1TyjvjLfaJIoc-Z6RqKnpxbhlcq6z3-d6HG-r-TKA2Do/edit](https://docs.google.com/document/d/1TyjvjLfaJIoc-Z6RqKnpxbhlcq6z3-d6HG-r-TKA2Do/edit)

FEATURES:

| Story point | Feature short description | Affected Services |  |
| :--- | :--- | :--- | :--- |
|  | Creation of orders via kitchen-backend | Kitchen App, Kitchen Backend |  |
|  | Restricted login for non existing kitchens | Kitchen Backend |  |
|  | Restricted unauthorized access to pushOrder | Push Order, handleDeliverectWebhook \(fix\) |  |
|  | Order Items Processing refactoring | ProcesOrder, orderAIProcessing |  |
|  | MIQA | Kitchen App, Kitchen Backend |  |

MIGRATIONS:

| Story point | Migration name | Affected Storages | Date |
| :--- | :--- | :--- | :--- |
|  | 2020-12-20\(2\)-order-item-status-change-status-column | MySql |  |
|  | 2021-02-01-add-deliverect-channel-link | MySql |  |

##  Version 0.9.0; Release:

FEATURES:

### Square Up Integration

MIGRATIONS:

| Story point | Migration name | Affected Storages | Date |
| :--- | :--- | :--- | :--- |
|  | 2021-01-22-sync-kitchen-staff-member-table-to-bigquery | BigQuery, MySQL | 2021.01.22 |
|  |  |  |  |

HOTFIXES:

Added auto-sync for data modified via GS

| User Story | Services hotfixed | Branch | Date | Sprint |
| :--- | :--- | :--- | :--- | :--- |
| [https://app.asana.com/0/1176875688547201/1199641479164770](https://app.asana.com/0/1176875688547201/1199641479164770) | Mailgun, Push Orders | release/0.9.0 | 2021.01.23 |  |
| [https://app.asana.com/0/1176875688547201/1199657080448151](https://app.asana.com/0/1176875688547201/1199657080448151) | Mailgun, Push Order | release/0.9.0 | 2021.01.25 |  |
| [https://app.asana.com/0/1176875688547201/1199660244187876](https://app.asana.com/0/1176875688547201/1199660244187876) | gsSyncTable, gsUbereatsRawReportPaymentsDetails | development \(by mistake\) | 2021.01.26 |  |

## Version 0.8.0; Release: January 12, 2021

### Automatically dispatch couriers

From now on, the orders will be sent to the delivery provider \(currently Relay\) upon the order preparation start in the kitchen app \(when the Start button is pressed\) and will automatically be marked as "Ready" so that the courier can arrive ASAP..

If for any reason the order was not successfully sent to the delivery platform, the user of the kitchen app will be notified and will have to create this order manually.

The feature will be released gradually, starting with the LIC2 location.

## 

## Version 0.7.0; Release: December 16, 2020

### Skip order

We introduced a new order status - “SKIPPED”.

You can see orders that are skipped in the “Finished” orders section and on the history page.

This special order status will be displayed as a tag.

A user can manually skip an order and undo these actions.

Overdue orders are skipped automatically.

### Automatically skip orders that are overdue

If the order “prepare by” \(aka delivery time\) is 30 minutes in the past, and the order is not yet marked as ready for delivery, the order will be automatically marked as skipped.

### Showing order processing details

Now, whenever you open an old order - you will see its processing details including photos of the items, their validity status, and whether the items were marked as packed.

### Orders history page

We added the orders history page, so you can see all orders for a particular day. You can select a day to show using a calendar or go back and forth between days with the pagination buttons.

### Logout button

As simple as that - logout button. It logs you out.

## Version 0.6.0; Release: November 30, 2020

### UI improvements

#### Automatic scroll to new orders

#### Animation in the appearance of new orders

#### Automatic scroll to the selected order

#### Bug fixes

### Order items checklist

Now you have a checklist of all items that should be packaged within the order. All items can be marked as packaged regardless of the checking process. This way we can verify that all items are packaged before the order is finalized and marked as ready for delivery.

### Test orders creation

Now we can easily create test orders using the page /tesing-orders

### Show version of the app on the settings page

### Allow push app update through a web socket

Now, whenever we release a new version of the app, we can force all clients to reload and upgrade to the latest version.

### Reading orders by parsing Grubhub emails

This feature allows us to receive orders from Grubhub and Seamless without Ordermark or any other aggregator integration. This is particularly important for LES1 hub and Cayenne brand, which were not connected to Ordermark.

### Bug fixes in the integration of Deliverect and Relay

## 

## Version 0.5.0; Release: November 12, 2020

### Responsive design and support of mobile devices

The layout of the application changes according to the screen size of the device that it is open on. Now the application is usable on mobile devices and tablets with vertical screen alignment.

### New orders highlighting

Orders that have not been open yet \(on a device\) will be highlighted with a red border and a red dot will be displayed on top of the “New” tab. The same behavior will be for orders that are new to the “In Progress” tab.

Note: after reloading the app, all orders will be automatically marked as opened and thus will not be highlighted. So only orders that came after the app was opened will be marked.

### UI fixes and bug fixes

* Position of notification messages is set in a way, to not cover useful buttons on the screen
* Now you can close the notification message without waiting for it to close automatically
* Bugfix: when pressing “Start” on a new order, it won’t get stuck
* Improved and more informative error messages

## 

## Version 0.4.0; Release: November 2, 2020

### Fullscreen mode

In the left bottom corner of the screen, you can find a “fullscreen” button, that will enable the fullscreen mode. This feature allows utilizing 100% of the spaces available on the screen.

### Control the list of kitchen staff members

You can control the list of employees at the kitchen using this [spreadsheet](https://docs.google.com/spreadsheets/d/1NQsdloTOxlvPw5P0YF_IdDasy9dPyU07bgURIz9pvps/edit#gid=0)

### Layout improvements and bug fixes

* Scrolling behavior was improved to prevent accidental page reloads
* Spacing between elements was fixed for improved consistency and more vertical space

## 

## Version 0.3.0; Release: October 28, 2020

### New UI

The kitchen app now has a new user interface, with improved styling and usability.

### Progressive Web App

Now the Kitchen App can be installed as an application on android. When installed this way, you can open the app from the home screen and it will look and feel like a native app. From now on, this is a preferred way to use the app.

### Login page

Now authentication to the kitchen app is done through a convenient login form.

### Audible notification upon a new order

Whenever a new order comes in - there is an audible notification.

### Selection of the supervisor and quality checker

Added new roles: supervisor and quality checker.

Now you can select the supervisor and quality checker once, and this selection will be automatically applied to each order when started.

### Detailed order information

Now you can see detailed order information through the kitchen app, including items, modifiers, and customer’s notes.

### Order processing cancellation

If you accidentally “started” the order - that’s not a problem anymore, because you can cancel this action with one click.

### Checked item image preview

After checking an order - the image of the item is previewed.

### Devices status page

A page that shows the status of all the devices in the kitchen: cameras, scales, and printers.

### Improved and more informative error messages

If anything goes wrong - you can see detailed information about what went wrong. This information can be used for troubleshooting.

### \[TECH\] API refactoring

REST API implementation instead of WS API.

Standardization and documentation using Swagger.

## 

## Version 0.2.0; Release: October 7, 2020

### Single selection of the main menu builder

Now you can select the menu builder once, and this selection will be automatically applied to each order when started.

### Integration of Intercom

Now you can send messages to mealco HQ directly from the kitchen app. You can use to report issues, ask for help, and coordinate actions with other hubs.

### Integration of HotJar screen recording

The screen of the Kitchen app is recorded, so that we can track usage habits and troubleshoot problems.

### 

