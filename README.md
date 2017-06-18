# Website Performance Optimization

##Instructions
1. Download the repository
2. Open _index.html_
3. Use ngrok to tunnel to the web and run Google PageSpeed and validate performance.
4. Return to _index.html_ and click the link to _pizza.html_
5. Open DevTools and the Console and observe the performance of the page.

##Outline

###index.html - Google PageSpeed Insights 90+ Score Methodology
I compressed my images using Google's compression tool to ensure optimization.
The profile picture was not that oversized, however, in devtools, I could see
that the pizzeria file was enormous.

Additionally, I reduced the file size of the JS and CSS files by allowing the
PageSpeed tool to remove unused styles and scripts to reduce the file size.
I also asynced any render blocking JavaScript and did some research to locate a
common script used to load web fonts in JavaScript and reordered the external file
calls after reviewing the page audit.

I used ngrok (after reading documentation) to tunnel the page for PageSpeed analysis.

In the end, my browser is displaying a **96** Desktop Score and **95** Mobile Score.


###pizza.html & views/main.js - Jank Removal
For _pizza.html_, I ran a preliminary analysis in DevTools to determine where jank
may be occurring. To do this, I recorded everything -- including page loads, button clicks, pizza slides, and scrolls and mouse events.

I was able to determine that the pizza slider was causing jank and
effectively used the knowledge gained by the course lesson to realize the code was
repeating itself and that it was unnecessarily complicated. I simplified the code so
that the slider used the switch statement to relatively size the pizza and regenerate
the pizza size using a for loop, which iterates through all of the pizzas and adjusts
them according to the slide position.

Additionally, I rewrote the _updatePositions_ script and the pizza generation code to
force calculations to occur outside of the for loops. Instead of using scrollTop, I set
a value of 0 for initial scrolling and then update this number as the user scrolls, to
simplify the calculation. To keep it from running repeatedly, I created a new value, which is now called in the for loop.

Finally, I changed the number of pizzas generated to reflect the viewport height / 33.3, which is the container height for the screen. I tested it, and pizzas filled the screen
no matter the size when the page was loaded, but when expanding the viewport, it was
clear that extra pizzas were not generated.

I also improved performance by changing the use of _querySelector_ to _getElementById_ and _querySelectorAll_ to _getElementsByClassName_, at the suggestion of the reviewers.

To validate my changes, I reviewed in DevTools and the console code driven by the
timing scripts.
