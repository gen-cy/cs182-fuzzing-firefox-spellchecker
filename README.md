# cs182-fuzzing-firefox-spellchecker
fuzzing firefox spellchecker (essentially fuzzing hunspell)

Software under test(really crude naming scheme):
Hunspell, the spellchecker used on Firefox.
File: hunspellexample.c (its a cpp file)

Hunspellexample.c takes in an argument (file with input to test). Then these inputs are then saved into a file to work with AFL++, so we can view what inputs have been checked.
It also displays the suggestions (considered invalid) if there are suggestions to the input.


Binary file after instrumentation: 
File: hunspellbin2

Stuff needed:
AFL++, compile it
Hunspell, compile it or install the package

Docker can be used, but there are issues with instrumentating the cpp file as the hunspell libraries are not found, so it is recommended to build AFL++ to run `afl-c++` then `afl-fuzz.`
