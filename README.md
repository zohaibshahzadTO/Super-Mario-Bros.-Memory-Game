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
