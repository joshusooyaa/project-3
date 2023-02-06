# UOCIS322 - Project 3 #
Author: Josh Sawyer

Email: jsawyer2@uoregon.edu

---

## Overview

The program is a simple anagram game designed for English-learning students in elementary and middle school. It presents a list of words to students and an anagram. The anagram is a jumble of some of the words, which are randomly chosen. Students attempt to type words that can be created from the jumble. When a matching word is typed, it is added to a list of solved words.


## flask_vocab.py

Changes made to `flask_vocab.py` introduces AJAX implementation. Now, flask_vocab can send information back without updating the page. Better put, whenever an answer is 'submitted', Flask no longer sends back an updated html file (using Jinja) and instead sends back a JSON response to the javascript in the html file that requested a JSON response ($.getJSON). 

`flask_vocab.py` gets a JSON request from the Javascript in the `vocab.html` page on each keydown. The goal is to check to see whether or not the text that has been passed to `flask_vocab.py` is a valid vocab word from the list. `rslt` which is the variable that is returned from `flask_vocab.py` is returned through flask.jsonify(). rslt holds to "JSON" variables, `response` and `txt`. `response` is very important for how the JavaScript handles what happens next, and should be 'match' when the text that was passed is a correct word. If the word has already been found, `response` should be "found", if there isn't a match (but it's a word from the list), `response` is "incorrect". If there isn't a match, then `response` it should be "none", although anything can work here since this is the last case that the Javascript handles and doesn't check then. Looking at `txt` this simply just allows for the Javascript to put error messages or warnings to the user about their input. For example, if `response` is "incorrect" or "found" then `txt` that is returned in the JSON file will contain the message that will be put onto the html page. Once all words have been found, `response` gets a string of "done".


## vocab.html

Changes made to `vocab.html` - now uses Javascript/AJAX to allow for updates to the HTML without refreshing the page. 

The JavaScript first removes the default action of an entry so it no longer refreshes the page. It then handles every single input into the text box by sending a getJSON request which is handled by `flask_vocab.py` and a JSON response is returned. In the JSON, `response` and `txt` is extracted as JavaScript variables, `response_txt` (txt) and `rsval` (response). `rsval` is then checked against several cases, and depending on which one, the response element in the html is updated to have all the correctly guessed words, or the error element of the page is updated to let the user know that what they inputted was either wrong, or already guessed. Once rsval == 'done' the page is redirected to the success page using window.location.href = "/success"


