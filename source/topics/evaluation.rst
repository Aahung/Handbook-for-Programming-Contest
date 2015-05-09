
Evaluation
============

------------------
Expression Forms
------------------

Normally there are three forms of expression:

- Infix (daily life)
- Prefix
- Postfix

^^^^^^^^^^^^^^^^^^^^^
Infix
^^^^^^^^^^^^^^^^^^^^^

Infix expression has this form :math:`(a + b) \times c`, we are familiar with
this form and we use it every day, while it is not friendly when we want to
evaluate it :-(.

^^^^^^^^^^^^^^^^^^^^^
Prefix
^^^^^^^^^^^^^^^^^^^^^

Prefix expression has this form :math:`\times + a b c`, which operator goes
first, then operands.

^^^^^^^^^^^^^^^^^^^^^
Postfix
^^^^^^^^^^^^^^^^^^^^^

Postfix expression has this form :math:`a b + c \times`, which operator goes
after operands.

----------------------
Expression Evaluation
----------------------

Among the three forms, Infix is the hardest to evaluate, and the other two
are relatively easy.

^^^^^^^^
Postfix
^^^^^^^^

1. Create a stack to store operands
2. Scan the expression from left to right, token by token

   - if the token is an operand, push it to stack
   - if the token is an operator, pop the operands and
     apply operetor to the operands in the stack and
     push the result back to stack

Here is an example, the operands are single-digit integers, and operators are ``+ - * /``.

::

  #include <stdio.h>
  #include <stack>
  #include <string.h>

  bool is_operator(char character) {
      if (character == '+' || character == '-'
            || character == '*' || character == '/')
          return true;
      else
          return false;
  }

  int perform_operation(char the_operator,
        int operand_left, int operand_right) {
      if (the_operator == '+') return operand_left + operand_right;
      else if (the_operator == '-') return operand_left - operand_right;
      else if (the_operator == '*') return operand_left * operand_right;
      else return operand_left / operand_right;
  }

  int evaluate_postfix(char *expression) {
      int length = strlen(expression);

      std::stack<int> operands;
      for (int i = 0; i < length; ++i) {
          if (is_operator(expression[i])) {
              int operand_right = operands.top(); // right comes first
              operands.pop();
              int operand_left = operands.top();
              operands.pop();
              operands.push(perform_operation(expression[i],
                            operand_left, operand_right));
          } else {
              operands.push(expression[i] - '0');
          }
      }
      return operands.top();
  }

  int main() {
      char expression[] = "12+3*4+";
  	  printf("%s = %d\n", expression, evaluate_postfix(expression));
  }

and the output is::

  12+3*4+ = 13

^^^^^^^^^^
Prefix
^^^^^^^^^^

Similar to postfix.

^^^^^^^^^^
Infix
^^^^^^^^^^
Translate into postfix then evaluate it. (smart)
