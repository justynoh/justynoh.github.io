---
layout: page
title: SML compiler
permalink: /projects/sml-compiler/
---

_[back to projects](/projects/)_

For a class on compiling higher-order typed languages, I implemented the type-directed translations for a compiler from Standard ML (SML) to C, written in SML. The front-end (parsing) and back-end (pointer allocation and writing to file) phases were not part of the project.

The input was the ast for SML code. First, the ast was typechecked based on the definition of SML. Then, features were elaborated out into a simpler language. For example, pattern matching was elaborated into a sequence of exception handlers and datatypes were elaborated into existentials with constructors and destructors. This then underwent phase splitting where each module was separated into its static components (i.e. constructors) and dynamic components (i.e. values), and these were packed into existential values. With no more modules, the direct-style code could then be converted into continuation passing-style code, which ensures that the eagerness of SML is correctly reflected in the compiler output. At the same time, this allows us to convert expressions into values. Next, lambdas were then converted into function closures which keep a context of environment variables around. The function closures could then hoisted out to the top level. This resulted in a sequence of functions whose variables could then be allocated with tags and code generated for each function.

Separately, a simple runtime system was also implemented in C along with a Cheney scan semi-space garbage collector.