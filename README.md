# cs182-fuzzing-firefox-spellchecker
fuzzing firefox spellchecker (essentially fuzzing hunspell)

Software under test(really crude naming scheme): <br>
Hunspell, the spellchecker used on Firefox. <br>
File: hunspellexample.c (its a cpp file) <br>

Hunspellexample.c takes in an argument (file with input to test). Then these inputs are then saved into a file to work with AFL++ to be mutated, so we can view what inputs have been checked.<br>
It also displays the suggestions (considered invalid) if there are suggestions to the input.


Binary file after instrumentation: <br>
File: hunspellbin2

Stuff needed: <br>
AFL++, compile it <br>
Hunspell, compile it or install the package

Docker can be used, but there are issues with instrumentating the cpp file as the hunspell libraries are not found, so it is recommended to build AFL++ to run `afl-c++` then `afl-fuzz.`

Run <br>
```afl-c++ -fsanitize=address,undefined -g -lhunspell-1.7 ./hunspellexample.c -o hunspellbin2 -Wall `pkg-config --cflags --libs hunspell` -Wall``` to compile and be eligible for instrumentation

Run <br>
```afl-fuzz -i in -o out4final -m none -- ./hunspellbin2 @@``` to start fuzzing.

Side note: on output_results_extra.tar.gz <br>
This contains two files that parsed the original input file to find what inputs were valid and invalid (i.e. words that Hunspell believes needs suggestions or are completely unfixable). <br>
There is also the frequency of the valid inputs in there, on ascending order.
The binary file will not run as it was compiled on ARM systems.

Results:
![image](https://user-images.githubusercontent.com/56899845/206831650-c15c486a-ae06-4011-9350-5e653697daa4.png)
