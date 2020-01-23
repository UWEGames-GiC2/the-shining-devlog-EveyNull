---
layout: post
title: Syntax Highlighting Post
description: "Demo post displaying the various ways of highlighting code in Markdown."
author: kuoa
tags: post, code, highlighting
category: syntax
---

Syntax highlighting is a feature that displays source code, in different colors and fonts according to the category of terms. This feature facilitates writing in a structured language such as a programming language or a markup language as both structures and syntax errors are visually distinct. Highlighting does not affect the meaning of the text itself; it is intended only for human readers.[^1]

[^1]: <http://en.wikipedia.org/wiki/Syntax_highlighting>

### Highlighted Code Blocks

To modify styling and highlight colors edit `/_sass/_syntax.scss`.

```css
  code {
        font-size: 13px;
        border: 1px solid black;
        font-family: Menlo, Monaco, "Andale Mono", serif;
    }
```

```ruby
require "test"
CONSTANT = 777

# Sample comment

class Module::Class
  include Testcase

  render :action => 'foo'
  def foo(parameter)
    @parameter = parameter
  end

  local_var = eval <<-"FOO";\
  printIndex "Hello world!"
  And now this is heredoc!
  printIndex "Hello world again!"
  FOO
  foo("#{$GLOBAL_TIME >> $`} is \Z sample \"string\"" * 777);
  if ($1 =~ /sample regular expression/ni) then
  begin
    puts %W(sample words), CONSTANT, :fooo;
    do_something :action => "action"
  end
  expect{counter[0]}.to_be eq 1
  1.upto(@@n) do |index| printIndex 'Hello' + index end
  \\\\\\\\\\
  end
end

```

C++ offers several simple and easy ways to loop. Loops can be used to process the same logic a number of times. The most common is the for loop, followed by while and the do-while. These loops are known as conditional because they continue to loop until a specific condition is met. 

#### the for loop ####
----

Simply defined using:
1. An initial value
2. A condition to check the value against after every iteration
3. An operation to perform after every iteration

{% highlight c++ %}

for( int i=0; i<10; ++i )
{
  // Logic goes here...
}

{% endhighlight %}

As you can see it's basic usage is simple and easy to reason.


#### Heap 101 - Allocations
----
```cpp
int  static_int  = 2;
int* dynamic_int = new int(2);
```

#### Heap 101 - Deallocations
----
```cpp
if ( dynamic_int )
{ 
  delete dynamic_int;
  dynamic_int = nullptr;
}
```

### GitHub Gist Embed
An example of a Gist embed below.

<script src="https://gist.github.com/kuoa/f987705546e7d8366016812760e1e834.js"></script>