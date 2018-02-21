# Super Mario Bros. Memory Game

The premise of the game is to have a grid of 24 face-down cards. The card faces consist of pairs of matches. Clicking on cards will flip them over, revealing the value. When two are chosen, if it’s a match, both cards will disappear. If it’s not, the cards will flip back over to face-down. The game should be different every time the game is refreshed.

# Planning

Before writing any code, we need to get an idea of the actual steps to take to go from nothing to finished product. Building this whole game at once might seem a bit overwhelming, but if you break it into small tasks, each task will seem achievable until it’s done.

<li>Display 12 cards.</li>
<li>Duplicate the cards to have 2 sets of 12.</li>
<li>Randomize the display of cards.</li>
<li>Add selected style for selected cards.</li>
<li>Determine if two selected cards are a match and hide them.</li>
<li>Only allow two cards to be selected at a time.</li>
<li>Reset guess count after 2.</li>
<li>Add delay to selections.</li>
<li>Show back of card initially and flip on select</li>
<li>Finished game!</li>

# CSS

We’ll add some basic styles, just enough for the app to make sense. No frameworks or unnecessary code here, or even any preprocessors. We're just creating a flex grid with cards. Each card is 150×150, and has background properties because we’ll be adding the card images soon as background images. This CSS will be adjusted as we add a few more complex features to the code, like card flipping.

# Step 1

The first step is to display 12 cards, each with a different value. To do this, I’m going to create an array of objects, and put it in the cardsArray variable. Each object will contain a name and an image.

Now we have 12 cards, but how do we display them? First, we’ll grab the element we said would be the root for the entire app – the div with an id of game. We’ll create a new section element, give it the grid class, and append it to the DOM inside our game root div.

If you take a look at the script.js file at this commit, you'll see that all we did was add a section to the DOM.

Now we want to get the images to display on the front end. We’ll loop through each item in cardsArray with forEach(), create a new card div for each object, and set the data-name attribute and background-image style property of the div. We will then append that div to the grid. This will give us 12 divs in total.

So, what’s the point of the data-name attribute? Data attributes allow us to store extra data in an HTML element. Any non-standard attribute should begin with data-.

At the end, each div (card) in the grid will look something like this :

<b><div class="card" data-name="shell" style="background-image: url("img/blueshell.png");"></div></b>


# Duplicate the cards to have 2 sets of 12

Step two is much simpler than step one. Now we’re going to duplicate the cardsArray array, then loop through that instead. First, below the array, we'll create a gameGrid variable, and duplicate the array by using concat().

# Randomize the display of cards

To do this, we'll shuffle the array using sort() and Math.random(). Don’t get how that works? Here.

Place this code right after the declaration of gameGrid.

# Add selected style for selected cards

Now we should be able to select cards. We're just going to add a simple CSS style so we can see selected items easily.

We’ll add an event listener to the entire grid. Anytime an element is clicked, the selected class will be applied to it. Add this code to the bottom of script.js

Now every selected div will have a blue border, as defined by the selected CSS.

# Only allow two cards to be selected at a time

We need to only allow two selections at a time, because we’re testing if two selected cards match. In order to do this, we’ll need to store the guesses and counter somewhere. First we’ll just store the count.

# Determine if two selected cards are a match and hide them

Now we'll create some CSS for matches. I’m going to give them a red border to differentiate them, and remove the background image. Why would I do that instead of just removing them from the DOM? Because we need to preserve the space they used to be – otherwise, all the elements would shift and it would no longer be a proper memory game.

In addition, where we just had a count variable before, we’ll add a place to store the first and second guess as well.

I’m going to make a function for matching elements. This will just loop through all selected elements when called, then add the match class.

Now I have to call the match() function at the right time in the code. Back in our event listener, I’m going to assign the first and second guess to their respective variables. If they’re both not empty and match, the match() function will be called.

Now, the guesses don’t reset, so we can only select or match one thing at a time. But if we select two elements we know match, the proper CSS will be applied

# Problem

We've come across a problem. If we select the same element twice, it will consider it a match, because they both have the same data-name property. Obviously, that's not how the memory game works. We'll fix this first before moving on.

By creating a variable called "previousTarget" and assigning null to it and then implementing that check to our return statement at the beginning at the top of the counter and then assigning the clicked value to "previousTarget" after the first click will disable the user from clicking on the same element twice.

# Reset guess count after 2

Currently, we only have two guesses. If they're a match, the match style will show. If they’re not, the regular selected style will show. We want to allow multiple guesses. We’ll have to do this by resetting the guess count after two guesses, whether they matched or not.

First, we’ll create a function to reset the guesses. This will set all counts and guesses back to their original values, as well as removing the selected CSS.

After doing that we can make multiple matches. You’ll notice that the select style will disappear immediately if it’s not a match, but this is fine because we haven’t set any delays to allow it to display longer.

# Add delay to selections for a little aesthetic appeal

Currently, when we click on any of the elements, the transitions happen immediately. We want a delay after we make a selection so the user can see what their selection was before the card is hidden again. Right now it doesn’t matter because everything is visible, but we can just take care of it before putting the final style touches on the cards.

We’re going to use setTimeout() to make the delays. First we’ll set my delay time, which we’re choosing to be 1200 milliseconds, or 1.2 seconds.

All we're going to do now is put the functions from before in the setTimeout(), with the delay variable as the amount of time for the timeout to last. The functions become callbacks now, which are functions used as arguments, and they no longer need the parentheses. Now if we open up a browser, we can see selections and matches for 1.2 seconds before they disappear.

# Show back of card initially and flip on select

When playing memory, all of the cards are usually shown to you all at once then flipped. You then have to use your memory in order to beat the game, hence the name of the game. Its better to do this step once you've added the functionality to the game.

The game has all the functionality we want, but not the styles. We need to:

<li>Hide the cards initially</li>
<li>Flip them over when selected</li>
<li>Make matches disappear</li>


All of this goes together, and will require a few structural changes to the code. We’ll have to add a bit more complicated CSS to get this done.

First, our cards have all consisted of one div right now. In order to implement the flip, each div will need to consist of three divs: card, front and back divs.

We’ll modify the card creation loop to add the front and back elements.

Where we had clicked.dataset.name and clicked.classList.add, we’ll have to add parentNode now, since we’ll be clicking on an inner div (front or back) and the data-name is still on the outer div (card).

Now we’re going to go back to CSS for a moment. To get the flip to work, we’re going to set each card as relative, and the back and front as absolute. All three will have the same height and width.

The front of each card (technically the back if you’re thinking like a deck of cards, but I’m calling it the front because it’s the default view) will be a question mark box.

The back will have all the properties for the background image to style property, and it will be rotated for the flip animation.

Selected items will be rotated, and matched items will become white, which will override the background image applied through JavaScript.

# Technology

HTML5, CSS3, Vanilla Javascript
