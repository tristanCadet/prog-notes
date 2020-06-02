# The web needs a new layout engine

###### Make it happen

I wish the web had a better layout engine. Just look at how easy it is to center an element with this constraint layout: http://www.layx.org/ `center = other_element.center`. I really like Layx's syntax, unfortunately this project didn't have any development in 5 years.

Now think about this: even though CSS has been around for 25 years we have to use a bunch of unintuitive hacks to layout things. CSS wasn't meant to do complex layouts but to style documents - which it does an ok job at, though markdown is better for simple use cases. The point is, if 25 years could not fix CSS layouts then we should explore other ways to layout stuff.   

We could argue that the web has no other usable layout engine. But what if we had spend 25 years polishing a layout engine instead of finding new ways to hack CSS ? We probably wouldn't have thousands of posts on how to center an element, some even cumulating millions of views (cf. stackoverflow). Seriously, this is sad. People must feel sorry for us: it took mankind a decade to send humans to the moon, but it's been 25 years and we still have no straightforward way to center an element. And don't get me wrong, it's not just about the centering, CSS layouts in general are leaky, incoherent, and behave unexpectedly. Heck, if a few people at major browsers' (Chrome, Firefox, Edge, Safari, Opera...) started to work on a new layout engine it wouldn't even take a year to have something that makes sense and is broadly usable.

If you are involved with a browser's development, making an efficient layout engine the new norm of the web is not just an act of kindness, it is also an investment in our future. It is thousands of thousands of developer's hours saved, in learning, understanding, debugging and refactoring layouts. It is increased security: since the layout code behaves as expected developers can easily spot bugs and avoid undefined behaviors. And it is probably saved compute time, especially if the DOM is replaced with a more efficient abstraction.

We have grown so used to hacks and bad practices that we do not even see them anymore. We should take a step back and wonder: "If I could build any tool I wanted to layout my website, would I build CSS ?" Probably not. 

You should use the right tool for the right job. 
If we care about web development, we should be pushing to have a better layout engine.