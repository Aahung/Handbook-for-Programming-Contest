
------------
I/O
------------

I/O exists in every program, in most cases it is easy, some cases are annoying.

I recommend you to use C instead C++ especially when the input or output is small.
The advantage of performance using C I/O is obvious, while C++ may handle some
situation quite friendly.

^^^^^^^^^^^^^
In
^^^^^^^^^^^^^

"""""""""
scanf
"""""""""

Reading from stdio, we often use ``scanf`` (`scanf doc`_).

For example::

  scanf("%d", &a_int); // read int
  scanf("%ld", &a_long); // read long
  scanf("%lld", &a_longlong); // read long long
  scanf("%llu", &a_unsignedlonglong); // read unsigned long long
  scanf("%f", &a_float); // read float
  scanf("%lf", &a_double); // read double

and of course, character array::

  char string[LENGTH];
  scanf("%s", &string);

"""""""""
gets
"""""""""

While if you want to read a whole line string containing spaces, ``scanf`` may not
be the best choice, and ``gets`` (`gets doc`_) is obviously better. (although some IDE will warn
you it is not safe, go to hell!)

Here is an example::

  char string[LENGTH];
  gets(string);

WATCH OUT!! In this case, special attentions: if the stdin is::

  1
  I am lucky!
  <EOF>

and the code is::

  int i;
  scanf("%d", &i);
  char string_unlucky[100], string_lucky[100];
  gets(string_unlucky);
  gets(string_lucky);
  printf("string_unlucky is: %s\n", string_unlucky);
  printf("  string_lucky is: %s\n", string_lucky);

You will get the output::

  string_unlucky is:
    string_lucky is: I am lucky!

try to figure out why.


^^^^^^^^^^^^^
Out
^^^^^^^^^^^^^

"""""""""
printf
"""""""""

Basically, we use ``printf`` (`printf doc`_) for put content to stdout.

.. _gets doc: http://en.cppreference.com/w/cpp/io/c/gets
.. _scanf doc: http://en.cppreference.com/w/cpp/io/c/fscanf
.. _printf doc: http://en.cppreference.com/w/cpp/io/c/fprintf

Just do it similarly::

    printf("%d", a_int);
