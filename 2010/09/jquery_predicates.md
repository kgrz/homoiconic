jQuery Predicates
===

With the [jQuery Combinators][comb] plug in, you can refactor if statements into fluent jQuery chaining calls. For example, given:

    var updated_killed_count = function (killed_stones) {
      // ...
      // some code updating a counter on the board
      // ...
      alert("Congratulations, you have killed " + killed_stones + ' stone(s).');
    }

You can turn this:

    var killed_stones = board
      .find('.killed')
        .removeClass('black white');
    if (killed_stones.length)
      updated_killed_count(killed_stones);

Into this:

    board
      .find('.killed')
        .ergo(updated_killed_count)
        .removeClass('black white');
        
That's nice: `.ergo` converts a test of existence into a guarded method call that chains fluently. However, sometimes you still want an old-fashioned `if` statement or anything else relying on testing existence. And if you are going to use something like an if statement to test for the existence of DOM elements, you might as well have some semantic sugar.

Thus, [jQuery Predicates][pred]. With jQuery Predicates in your jQuery quiver, you can replace this:

    if (killed_stones.length)
      updated_killed_count(killed_stones);
      
With this:

    if (killed_stones.exists())
      updated_killed_count(killed_stones);
    
And replace this:

    while (0 === stones.into(adjacents).length) {
      // ...
    }
      
With this:

    while (stones.into(adjacents).do_not_exist()) {
      // ...
    }

In short, [jQuery Predicates][pred] adds two queries to every jQuery selection: `.exists()` returns true if the selection has at least one element, and `.does_not_exist()` returns true if the selection is empty (for convenience, jQuery Predicates also defines the synonyms `.exist()` and `do_not_exist()`).

And naturally, jQuery Predicates plays well with jQuery Combinators. Using them together, you now have access to `.ergo()`, `.when()`, `.exists()`, and `.does_not_exist()` for discriminating between empty and non-empty selections.

Enjoy!

---

Recent work:

* [Kestrels, Quirky Birds, and Hopeless Egocentricity](http://leanpub.com/combinators) and my [other books](http://leanpub.com/u/raganwald).
* [Cafe au Life](http://recursiveuniver.se), a CoffeeScript implementation of Bill Gosper's HashLife written in the [Williams Style](https://github.com/raganwald/homoiconic/blob/master/2011/11/COMEFROM.md).
* [Katy](http://github.com/raganwald/Katy), a library for writing fluent CoffeeScript and JavaScript using combinators.
* [YouAreDaChef](http://github.com/raganwald/YouAreDaChef), a library for writing method combinations for CoffeeScript and JavaScript projects.

---

[Reg Braithwaite](http://braythwayt.com) | [@raganwald](http://twitter.com/raganwald)

[comb]: http://github.com/raganwald/jQuery-Combinators
[pred]: http://github.com/raganwald/jQuery-Predicates
