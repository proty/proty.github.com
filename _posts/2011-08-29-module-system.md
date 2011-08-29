---
author: Thomas Gatzweiler
title: Module System
layout: post
---

Almost all of the programming languages out there require explicit
statements to import a module. This often leads to files with a lot of
import statements at the top, which have to be updated to add or
remove a module. But is this really necessary, can't the compiler do
this job?

Proty implements this with a strictly seperated namespace for modules,
so the compiler could determine all used modules at compile time. Each
module access consists of the module name, a colon and the name of the
module member. This is a simple example:

{% highlight erlang %}
io:print("Hello World")
{% endhighlight %}

To compile this statement to an executable the compiler checks whether
the module `io` is loaded yet and links it in if necessery. If you
compile this statement to a module itself, the compiler loads the `io`
module temporarily, to check whether the used objects (in this case
the function `print`) of this module exist, and adds the `io` module
to the `deplibs` of the generated LLVM-module. The generated code for
this compiled module looks like this:

{% highlight llvm %}
; ModuleID = 'helloworld.bc'

deplibs = [ "pr:io" ]

@.str = internal constant [12 x i8] c"Hello World\00"
@pr_io_print = common global %struct.Object* undef

define void @helloworld_init() {
entry:
  %0 = load %struct.Object** @pr_io_print, align 8

  %stringtmp = call %struct.Object* @String_new(i8* getelementptr inbounds
     ([12 x i8]* @.str, i64 0, i64 0))

  %calltmp = call %struct.Object* (%struct.Object*, i32, ...)*
                   @Object_call(%struct.Object* %0,
                                i32 2,
                                %struct.Object** @Qnil,
                                %struct.Object* %stringtmp)
  ret void
}
{% endhighlight %}
