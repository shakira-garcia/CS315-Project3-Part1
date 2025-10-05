Student Information

Name: Shakira Garcia

Student ID: 008218438

Repository Link: https://github.com/shakira-garcia/CS315-Project3-Part1.git

Collaboration & Sources
- This project is my work except for the code that was already there (main.cpp)
-Starter utilities (utils.hpp/.cpp, script paths on Blue) were provided
- Online references used:
https://www.geeksforgeeks.org/cpp/file-system-library-in-cpp-17/
https://www.geeksforgeeks.org/cpp/tokenizing-a-string-cpp/
https://www.geeksforgeeks.org/cpp/read-input-until-eof-in-cpp/
https://www.geeksforgeeks.org/cpp/namespace-in-c/
- ChatGPT helped me with my comments (clarifying wording and organization of explanations).
- I reviewed and adapted all comments to match the assignment’s constraints and my own understanding.

Implementation Details
Scanner.hpp/.cpp — Scanner class that scans the input and returns tokens

Goal: Read one .txt file and write tokens to input_output/<base>.tokens.

Scanner design (Part 1 only):

Tokens: sequences of ASCII letters a–z/A–Z, lowercased.

Apostrophes: kept only if internal (between two letters), e.g., can't.

Separators: all non-letters (digits, punctuation including hyphens/dashes, whitespace, non-ASCII).

readWord(std::istream&): skips separators, collects one token, returns "" if none.

tokenize(std::vector<std::string>&): fills the vector with tokens from the file.

tokenize(..., outputPath): runs tokenize then writes one token per line.

Design

Scanner stores the input file path and provides:

error_type tokenize(std::vector<std::string>& words);
Reads the entire input and fills words.

error_type tokenize(std::vector<std::string>& words, const std::filesystem::path& outputFile);
Same as above, then writes one token per line to outputFile.

std::string readWord(std::istream& in);
Reads the next word: skips separators, collects letters, keeps an apostrophe only if it’s internal; returns "" when no more tokens can be read.

Lowercasing: done character-by-character for letters.

Lookahead logic: uses in.peek() (stored as int c) so it can distinguish valid bytes from EOF.



Note discovered in main.cpp:
I found and fixed a construction issue so Scanner uses the input .txt, not the output .tokens.

Testing & Status

How I tested

Local compile/run with:

g++ -std=c++20 -Wall *.cpp -o huffman_part1
./huffman_part1 input_output/sample.txt


Blue scripts (compile_and_test.bash + copy_files.bash) using multiple sample files. The script compiles, runs, and diffs input_output/<base>.tokens against the reference tokens in:

/home/faculty/kooshesh/cs315_f2025_p3_part1/part1_tokens_files/


What works:

CLI requires exactly one argument (the input .txt path).

Checks input_output/ exists; checks input file exists; checks output file is writable.

Tokenization rules per spec (letters only, internal apostrophes allowed, lowercase).

Writes input_output/<base>.tokens with one token per line.

Build
g++ -std=c++20 -Wall *.cpp -o huffman_part1
./huffman_part1 input_output/your_input.txt
On Blue (Part 1 — Scanner)
One-time per project directory:

bash

cp /home/faculty/kooshesh/cs315_f2025_p3_part1/compile_and_test.bash .
cp /home/faculty/kooshesh/cs315_f2025_p3_part1/copy_files.bash .
Copy the sample inputs:

bash
bash copy_files.bash
# This puts sample .txt files into input_output/
Compile, run, and compare one file:

bash
bash compile_and_test.bash call_of_the_wild.txt