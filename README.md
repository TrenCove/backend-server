This is the backend for the e-commerce system for EECS 4413.

# Getting Started

First, install all dependencies

```bash
npm install
```

Second, compile the server and run the server

```bash
npm run build
npm run start
```

#### NOTE: 

There is a known bug with the sqlite3 node module that will fail to install properly when switching from different architectures (Mac/Windows/Linux).
If this error occurs, please run the below command to reinstall the correct sqlite3 module for your architecture

```bash
npm uninstall sqlite3
npm install sqlite3
```

Third, run the web server. The webserver can be found [here](https://github.com/TrenCove/frontend-site) or within the `/frontend-site/` folder bundlded together.

To run the web server, please run within that directory

```bash
npm install
npm run build
npm run start
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the website.

# Website navigation instructions

## Homepage and item display/search page
http://localhost:3000

Within this page, there are 2 buttons to create dummy test Dutch and Forward auction items. There is also a search bar to search for items on the table.

For Dutch items:
- The price automatically decreases every 1 minute by 10%.

For Foward items:
- The time is automatically set to end 5 minutes from when the item is created.

## Login Page
http://localhost:3000/login

Within this page, you can login to the webpage, you may use the test account:
Username: test
Password: password

## Signup Page
http://localhost:3000/signup

Within this page, you can signup to the webpage, please provide all needed fields as there is currently no error checking on the web side.

## Item Page
http://localhost:3000/item/[id]

These are the item pages, the id corresponds to an item id. On this page, it displays all the items and users can bid or buy an item.

This webpage connects to the backend via websocket to provide real time updates to all viewers of the item whenever a bid occurs or the time ends.
Whenever a user visits the webpage, they are subscribed via websocket to notifications, when any user bids or buys, it sends a publish request to all users
to update their webpage. For Dutch items, this is whenever someone buys, for Forward auctions, this is whenever anyone bids, or automatically after 1 minute to check for the timer.

NOTE: It currently takes a few seconds for the webpage to connect to the websocket, so if an action is performed immediately after landing to the page, it will not publish properly.


Once an item is bought or the timer ends, the user is shown a form to enter their card details to buy, they can also check the expedited shipping. After buying, they are directed to the receipt page.

## Receipt Page
http://localhost:3000/receipt/[id]

This is the receipt page, it will show the receipt for the corresponding item id
