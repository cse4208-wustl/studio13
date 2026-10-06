# Studio 13

## Template Argument Deduction

In this studio, you will explore how the compiler deduces template argument types, the type conversions that may occur during deduction, and how explicit template arguments can be provided to allow specific instantiations (including overcoming ambiguity that may arise from overloading). You will also use the type transformation templates provided by the `<type_traits>` library, including the one that is essential to the implementation of the `std::move` function template used in earlier studios.

## Collaboration

You may complete this studio individually or in a small group.

## Reference

If you need a refresher on the environment setup steps from the previous studios, see [Studio 0](https://github.com/cse4208-wustl/studio0).

If you need the class and `main` function that this studio builds on, see [Studio 11](https://github.com/cse4208-wustl/studio11).

## Exercises

Record your answers in `ANSWERS.md` as you work. Include the names of everyone who worked on the studio in your first answer, and number your responses so they are easy to match to the exercises.

1. List the names of the people who worked together on this studio.

2. SSH into `shell.cec.wustl.edu` using your WUSTL Key credentials, then use `qlogin` to connect to one of the Linux Lab machines and confirm that the version of `g++` there is correct, as you did in [Studio 0](https://github.com/cse4208-wustl/studio0).

   Clone your `studio13` repo using SSH:

   ```bash
   git clone git@github.com:cse4208-wustl/studio13.git
   cd studio13
   ```

   The repo already includes a `Makefile`. Copy the source (`.cpp`) and header (`.h`) files from your completed [Studio 11](https://github.com/cse4208-wustl/studio11) work into this repo and rename them as appropriate (for example, `studio11.cpp` to `studio13.cpp`). Update the `Makefile` as needed so it builds an executable named `studio13` from the source and header files in this repo.

   Confirm that your program builds and runs. In your answers, show the output that your program produced.

3. Add a template header file and a template source file to this repo, and in them declare and define a function template that is named something other than `move` and is based on the code shown in the lecture slides to illustrate the implementation of `std::move`. Make sure that the template header file includes the template source file.

   Update the `Makefile` with the names of those files in the appropriate lines, and update the source file for your `main` function so that it:

   1. includes the template header file
   2. replaces all calls to `std::move` with calls to the function template you just declared and defined

   Compile and run your program and confirm that it produces the same output as in the previous exercise. In your answers, show all the lines that used to call `std::move` and that now call your function template instead.

4. In `main`, replace all calls to operator `new` that are then used to initialize a `std::unique_ptr` with calls to `std::make_unique` instead. See the [documentation of `std::make_unique`](https://en.cppreference.com/w/cpp/memory/unique_ptr/make_unique) (which was introduced in C++14) for syntax and other details.

   Compile and run your program and confirm that it produces the same output as in the previous exercise. In your answers, show all the lines that used to call `new` and that now call `std::make_unique` instead.

5. In the source file for your `main` function, include the `<typeinfo>` and `<type_traits>` library header files.

   In `main`, use the `std::remove_reference` type transformation template to print out the name of the type that is pointed to by the `std::unique_ptr`. Specifically, after the statement that uses `std::make_unique` to initialize it, wrap a dereference of the `std::unique_ptr` variable within a `decltype` specification and use that expression to declare a variable of type `std::remove_reference<decltype(*up)>::type`, where `up` is the name of the `std::unique_ptr` variable.

   Then use the `typeid` operator, and the `name()` member function of the `std::type_info` object it returns, to print the name of that variable's type to the standard output stream, as in:

   ```cpp
   cout << typeid(v).name() << endl;
   ```

   Build and run your program. In your answers, show the type name that was output.

## Deliverables

Commit and push all modified and added files, including `ANSWERS.md`, to the repo.
