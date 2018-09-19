# Hypnotic Spiral 5.1
Copyright (C) 1998-2018 by ultracon0 (stopthedeepweb@protonmail.com)

originally by

Yonah Arakoslav
arakoslav@protonmail.com


The program is made to be very easy to use.  It should be able to get
out of your way and get its job done.

### Installation

This program is written in a language called Python, and heavily uses
a library for Python called PyGame.  To use this program, you'll have
to install both of them.  You can get Python from
<http://www.python.org/download/> and PyGame from
<http://www.pygame.org/download.shtml>. this program is best run on macOS 10.12 or newer , it may run on older versions or on windows, but this is not officially supported.

You will also need media.  Put pictures in the "images" directory.  included images may or may not exist

You can replace the included MP3 files if you like.  In fact, you'll
have to!  To cut down on size, not all MP3 files are supported.

After that, you can just run spiral.py:

> python spiral.py

If you make it executable, Windows or Mac machines should be able to
just double-click it:

> chmod a+x spiral.py

### Usage

The program may prompt you with information you must acknowledge to
proceed.  Read it and just hit return.

It may ask you questions, requiring either yes/no or short text
answers.  You can press "y" or "n" to answer the simple questions, or
just type an answer to later questions.  It *should* handle non-ASCII
characters properly, but I don't use that often and so haven't tested
it as much.

While it's running, you can press single keys to change some
behavior.  "<" or ">" will adjust the speed, as will their unshifted
equivalents "," or ".".  "f" will toggle fullscreen mode, and "i" will
toggle the background images.  "q" will quit the program.

The program can do those things on its own, too---sometimes a script
will cause it to go full-screen on its own, or to start showing you
pictures.

## Extending the program: writing scripts

I've included a number of example scripts in "config.py".  This should
make it easy to see what you can do.  There are a couple of points
worth mentioning:

You don't have to subclass Standard; it just catches you if you screw
up.  The top of config.py has utility functions.  You don't have to
use those either, though they can make things easier.  You should see
most of them used in the body of the work.

Running text is separated by any white space; the "words" helper
function turns words("foo bar baz") into ["foo", "bar", "baz"].
Nothing stops you from including spaces in words to display---I just
find whitespace works well as a separator.

Variables always start with "$" when used, and don't have the "$" when
you're assigning to them.  I don't guarantee you can pull off
double-substitution tricks like replacing $$role with Alice, where
$role=slave and $slave=Alice.  That particular version will work, but
only by accident.

Any string starting with ! will be interpreted as a command; see
Spiral.act_on for the evaluator.  It's pretty cruddy, but it does work
for this purpose.  Sometimes you'll want to make sure evaluation is
delayed until run-time.  For example, you don't care about whether the
music is playing when you *start* the program, but you'd like to check
whether it's on at this particular moment in the course of the run.
Put this material in quotes; it'll be evaluated at run-time.
You can see this in Standard:

        cond("self.draw_image",
             words("Turn on the pictures.  Hit the 'i' key.")) + \
             words("""You lust for the pictures. $name will be like the
             pictures. This turns you both on. You need the changes. You
             lust for the changes. $name will be changed. This is sexy. It
             would feel so good just to surrender to it.""") + \
        cond("not self.config.fullscreen",
             words("Feel so good to go fullscreen.  Hit 'f'."),
             words("So good to be fullscreen.  So good to be immersed.")) + \

If there were no quotes around self.draw_image, it would be checked
when the program started---no good at all.

The "alpha" values are for transparency.  "scale" adjusts the size of
the spiral, and "time_scale" the number of ticks that pass per frame.
"frequencies" controls how many ticks must pass before the spiral,
text, or images advance.  At the default setting, the spiral advances
every tick, the images every 10 ticks (5 frames because time_scale is
2), and the words every 20 ticks (10 frames).

Each config script will start with its "text()" method.  That's the
one thing you must override; the other names like "body()" are just
my convention.

Experiment!  Try new things and let me hear about them!  I'd love to
see new scripts or new uses for the program.  Let me know at
<yonah.arakoslav@yahoo.com>


## Extending the program: new modules

Right now, it's hard to add new things like subliminal text or a
"click me if you're not my mindfucked little hypnoslave" button that
goes away on its own.  I'd like to make it easier, but so far you're
pretty much on your own.

## My to-do list

I know there's more to do.  My progress with this program is driven by
my own desires.  I'm willing to entertain requests, but rather
unlikely to implement them---think of them as attempts at
inspiration.  If I'm inspired, I'll implement a requested feature.  If
not, I suggest *you* implement it and send a patch my way.  I'm very
likely to accept patches, integrate them, and redistribute them to the
community.

My own notes on what to do are at the top of the spiral.py file.

## About the Author

Yonah Arakoslav is a none-too-clever pseudonym.  I'm sure that with a
little work, you can figure out who I really am.  That's OK.  I just
don't want search engines fingering me.
