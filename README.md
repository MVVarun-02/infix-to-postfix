# infix-to-postfix

#include <stdio.h>

#include <stdlib.h>

#define SIZE 50


char s[SIZE];

int top = -1;

push(char elem) {

  s[++top] = elem;
  
}

char pop() {

  return (s[top--]);
  
}

int pr(char elem) {

  switch (elem) {
  
    case '#':
    
      return 0;
      
    case '(':
    
      return 1;
      
    case '+':
    
    case '-':
    
      return 2;
      
    case '*':
    
    case '/':
    
    case '%':
    
      return 3;
      
    case '^':
    
      return 4;
      
  }
  
}

void main() {

  char infix[50], posfix[50], ch, elem;
  
  int i = 0, k = 0;
  
  printf("\n\nEnter the Infix Expression ");
  
  scanf("%s", infix);
  
  
  push('#');
  
  while ((ch = infix[i++]) != '\0') {
  
    if (ch == '(')
    
    push(ch);
    
    else if (isalnum(ch))
    
    posfix[k++] = ch;
    
    else if (ch == ')') {
    
      while (s[top] != '(')
      
      posfix[k++] = pop();
      
      elem = pop();
      
    }
    
    else {
    
      while (pr(s[top]) >= pr(ch))
      
      posfix[k++] = pop();
      
      push(ch);
      
    }
    
  }
  
  while (s[top] != '#')
  
  posfix[k++] = pop();
  
  posfix[k] = '\0';
  
  printf("\n Infix Expression: %s \n Postfix Expression: %s\n", infix, posfix);

}
