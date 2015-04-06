# decluttter
App to declutter your life and then stuff.


Declutter is a platform for users to get rid of unused stuff or to get your friends’ unused stuff within the user’s private network of connections (think “a private Craigslist”). The site was created using Django with REST Framework on the backend, Angular and Bootstrap on the frontend and a SQLite database.

An overview of the Django apps:
-AppUser contains Stream and Follower classes. Stream was designed to tie together items and users to create our views for the Friends Crap stream. Follower was designed to be the table of follower-to-followee relationships. “Followee” is the user and “follower” is their friend. When a user starts following someone then the other person automatically starts following them.

-Items contains just an Items class for the items that users post or claim.

-Authentication contains the registration, verification, login, and authentication functionality.

Structure of the Angular views:
Home/Register/Login pages don’t require login authentication. If anyone tries to hit any of the other views they will only see the Home page.

Friends Crap - this view is a feed of the items your friends are trying to give away. Items will be dynamically added whenever a friends adds a new item. Users can “claim” an item if they want it. The “claim” button creates a patch trigger to add in the claimer data into the Item and update the Item’s availability to false (claimed). Users can also “hide” an item if they don’t want to see it in their feed. Note this is hiding the item for the user’s session only. The item will be back again the next time they log in.
The feed is created by nested API calls. Step 1 gets a list of all items from the Item API. Then an empty object initializes to add in the user and item details. Step 2 gets all the followers from the Follower API. Step 3 produces a resulting array of objects that is the list of items from your list of friends.

My Crap - this view is the list of items you currently have posted to give away (users can delete an item from here too) as well as links to views to add a new item and to see the list of items you have claimed from friends.
Add a New Item - adding a new item (name of item, description, and category) triggers a post request to the Items API to add the item to the list of items for that user.

My Claimed Items - this is a list of items owned by your friends that you have claimed for yourself. Items will be deleted from this view if the owner deletes the item.

My Friends - this view contains the list of friends you are already connected to as well as a link to add a new friend. Users can delete a friend off the list as well.
Add a Friend - friends get added to your friends list by entering the email of an existing user. This triggers a post request to the Follower API to add this new follower/followee and followee/follower relationship .

