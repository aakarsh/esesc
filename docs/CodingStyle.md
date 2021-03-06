
All  the  source  code has  the  same  coding  style. Please,  try  to
maintaing the same  style.  The coding style is  very simple, the same
that the Linux  kernel coding style, but with tabstops  set to 2. This
style  is also  very similar  to K&R.  With "indent  -kr -i2"  you get
similar results.

----------------------------------------------------------------------
Chapter 1: Indentation

Tabs are 2 characters (2 spaces,  not a tab \t), and thus indentations
are also 2 characters.


----------------------------------------------------------------------
Chapter 2: Placing Braces

The other issue that always comes  up in C styling is the placement of
braces.  Unlike  the indent size,  there are few technical  reasons to
choose one placement  strategy over the other, but  the preferred way,
as shown  to us by the prophets  Kernighan and Ritchie, is  to put the
opening  brace last  on the  line, and  put the  closing  brace first,
thusly:

    if (x is true) {
                  func(a, b, c);
      we do y
    }


Note that the closing brace is empty on a line of its own, _except_ in
the  cases  where  it  is  followed  by a  continuation  of  the  same
statement,  ie  a  "while"  in  a  do-statement or  an  "else"  in  an
if-statement, like this:

    do {
      body of do-loop
    } while (condition);

and

    if (x == y) {
      ..
    }else if (x > y) {
      ...
    }else{
      ....
    }
        

----------------------------------------------------------------------
Chapter 3: Naming

Descriptive names for  global variables are a must.   To call a global
function `foo` is a shooting offense.

If a word has a subpart with `max` or `min`, type max or min always at
the beginning of the word. Like in maxNumInst or maxMentalWonking.

GLOBAL variables (to  be used only if you _really_  need them) need to
have  descriptive  names, as  do  global  functions.   If you  have  a
function that counts the number  of active users, you should call that
`countActiveUsers()` or similar, you should _not_ call it `cntusr()`.

LOCAL variable names  should be short, and to the  point.  If you have
some random  integer loop counter,  it should probably be  called `i`.
Calling it `loop_counter` is non-productive,  if there is no chance of
it being mis-understood.  Similarly, `tmp`  can be just about any type
of variable that is used to hold a temporary value.

Composed names  for variables and functions begin  with lowercase, and
the    following     words/abbreviations    begin    with    uppercase
(e.g.   getMemoryObj).  Classes  and   constants  always   begin  with
uppercase.
		
----------------------------------------------------------------------
Chapter 4: Functions

Functions  should be short  and sweet,  and do  just one  thing.  They
should fit on  one or two screenfuls of text  (for a 124x50 terminal),
and do one thing and do that  well. (PLEASE NO MORE THAN 100 lines per
function)

If   you  have   a  complex   function,   and  you   suspect  that   a
less-than-gifted  first-year   high-school  student  might   not  even
understand what  the function is all  about, you should  adhere to the
maximum  limits  all the  more  closely.   Use  helper functions  with
descriptive names  (you can  ask the compiler  to in-line them  if you
think it's performance-critical, and it  will probably do a better job
of it that you would have done).

Another  measure of  the function  is the  number of  local variables.
They shouldn't exceed 5-10, or you're doing something wrong.  Re-think
the function,  and split  it into smaller  pieces.  A human  brain can
generally easily keep track of about 7 different things, anything more
and it gets confused.  You know you're brilliant, but maybe you'd like
to understand what you did 2 weeks from now.

----------------------------------------------------------------------
Chapter 5: Commenting

Use C++ comment style: `// bla bla bla`

Comments  are good,  but there  is also  a danger  of over-commenting.
NEVER  try to  explain HOW  your code  works in  a comment:  it's much
better to write the code so  that the _working_ is obvious, and it's a
waste of time to explain badly written code.

Generally, you  want your  comments to tell  WHAT your code  does, not
HOW.  Also, try  to avoid putting comments inside  a function body: if
the function is  so complex that you need  to separately comment parts
of it, you should probably go back  to chapter 4 for a while.  You can
make  small comments  to  note or  warn  about something  particularly
clever (or ugly), but try  to avoid excess.  Instead, put the comments
at the head of the function, telling people what it does, and possibly
WHY it does it.

Many times  much better than adding  a comment is to  add an assertion
(See Chapter 6).

----------------------------------------------------------------------
Chapter 6: Assertions

For all the code that you write always use `nanassert.h`.  This provides
an extension over  the traditional assert system. At  the beginning of
the function check for the  preconditions that you have assumed (don't
check for postconditions, it slowsdown the code too much).

This  is useful  in  several ways.   First,  it is  the best  possible
available documentation because it catches errors, it is upto date (or
it  does not work).  Second, it  reduces the  overhead of  checks. The
checks are  done only in  DEBUG mode. Don't  even care if  the program
crashes in non-debug mode. If  the simulation crashed, the way to find
the bug is to compile in debug mode an execute it.

All the code like that should be transformed to assertions. 

Original:
    if (pointer == 0) {
      printf("Error....");
    }
New:
    I(pointer);

----------------------------------------------------------------------
Chapter 7: Includes

Place system includes first using  `<...>`. Leave a blank line and place
sesc includes in ALPHABETICAL order includes `"...."`. Example:

    #include <stdlib.h>
    #include <strings.h>

    #include "Port.h"
    #include "TaskHandler.h"
    #include "TaskContext.h"
    #include "VBus.h"
    #include "VMemorySystem.h"

