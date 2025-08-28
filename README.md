# CMPS 2200  Recitation 01

**Name (Team Member 1):** Nikhil Modayur  
**Name (Team Member 2):**_________________________

In this recitation, we will investigate asymptotic complexity. Additionally, we will get familiar with the various technologies we'll use for collaborative coding.

To complete this recitation, follow the instructions in this document. Some of your answers will go in this file, and others will require you to edit `main.py`. All tests are in `test_main.py`.

## Install Python Dependency

We need Python library of "tabulate" to visualize the results in a good shape. Please install it by running 'pip install tabulate' or 'pip install -r requirements.txt' in Shell Tab of Repl.  

## Running and testing your code

- To run tests, from the command-line shell, you can run
  + `pytest test_main.py` will run all tests
  + `pytest test_main.py::test_one` will just run `test_one`
  + We recommend running one test at a time as you are debugging.

## Turning in your work

- Once complete, click on the "Git" icon in the left pane on repl.it.
- Enter a commit message in the "what did you change?" text box
- Click "commit and push." This will push your code to your github repository.
- Although you are working as a team, please have each team member submit the same code to their repository. One person can copy the code to their repl.it and submit it from there.

## Comparing search algorithms

We'll compare the running times of `linear_search` and `binary_search` empirically.

`Binary Search`: Search a sorted array by repeatedly dividing the search interval in half. Begin with an interval covering the whole array. If the value of the search key is less than the item in the middle of the interval, narrow the interval to the lower half. Otherwise, narrow it to the upper half. Repeatedly check until the value is found or the interval is empty.

- [X] 1. In `main.py`, the implementation of `linear_search` is already complete. Your task is to implement `binary_search`. Implement a recursive solution using the helper function `_binary_search`. 

- [X] 2. Test that your function is correct by calling from the command-line `pytest test_main.py::test_binary_search`

- [X] 3. Write at least two additional test cases in `test_binary_search` and confirm they pass.

- [X] 4. Describe the worst case input value of `key` for `linear_search`? for `binary_search`? 

The worst case input input value for linear_search would either be the last element in the list, or an element not present in a list. The same is true for binary search. 

- [X] 5. Describe the best case input value of `key` for `linear_search`? for `binary_search`? 

Best case input value for linear_search would be the first element in the list, and the worst case would be binary_search. 

- [X] 6. Complete the `time_search` function to compute the running time of a search function. Note that this is an example of a "higher order" function, since one of its parameters is another function.

- [X] 7. Complete the `compare_search` function to compare the running times of linear search and binary search. Confirm the implementation by running `pytest test_main.py::test_compare_search`, which contains some simple checks.

- [ ] 8. Call `print_results(compare_search())` and paste the results here:

|        n |   linear |   binary |
|----------|----------|----------|
|        1 |    0.001 |    0.001 |
|       10 |    0.000 |    0.001 |
|      100 |    0.001 |    0.000 |
|     1000 |    0.014 |    0.002 |
|    10000 |    0.136 |    0.002 |
|   100000 |    1.363 |    0.001 |
|  1000000 |   14.232 |    0.006 |
| 10000000 |  158.680 |    0.014 |

- [X] 9. The theoretical worst-case running time of linear search is $O(n)$ and binary search is $O(log_2(n))$. Do these theoretical running times match your empirical results? Why or why not?

Yes, the empirical results match the theoretical running times. As the input size n increases, the running time for linear search increases much more rapidly than for binary search. The binary search time remains almost constant which is expected from the $O(log_2(n))$ theoretical growth rate. 

- [X] 10. Binary search assumes the input list is already sorted. Assume it takes $\Theta(n^2)$ time to sort a list of length $n$. Suppose you know ahead of time that you will search the same list $k$ times. 
  + What is worst-case complexity of searching a list of $n$ elements $k$ times using linear search? 

    The worst-case complexity is $O(kn)$, since each search could take $O(n)$ time and you do $k$ searches.

  + For binary search?

    The worst-case complexity is $O(n^2 + k \log_2 n)$, since you must first sort the list ($O(n^2)$) and then each search takes $O(\log_2 n)$, for $k$ searches.

  + For what values of $k$ is it more efficient to first sort and then use binary search versus just using linear search without sorting? 

    It is more efficient to sort and use binary search when $n^2 + k \log_2 n < kn$, which simplifies to $k > \frac{n^2}{n - \log_2 n}$. For large $n$, this means binary search becomes more efficient when you have to search the list a lot of times ($k$ is large enough to offset the cost of sorting).