STA250HW2
=========
In this homework we evaluate the mean, standard deviation and median of flight arrival delay from several *.csv files, by taking parallel approaches.

Our first implementation is based on the R parallel package using the frequency table (histogram) method. Each call of function funFreqTable() is in charge of build a frequency table for each file by reading the file from standard input block-by-block. In our bash command, we use sed to handle the comma in the quoted field by simply removing it. When mapply() returns a list of frequency table, we combine them to get a grand frequency table.

Our second implementation is based on a task pool model implemented with pthread. Specifically, we build a structure entity called data, whose members include all the filenames of all .csv files, flag value indicating whether each file has been processed by a worker thread or not, and a frequency table for the files processed so far. We start several worker threads, each of which fetches an unprocessed file from data, compute its frequency table using fast sample method with sampling probability of 0.0002, and combine the result with the grand frequency table in the data entity. Upon accessing the file name and updating the grand frequency table, we need two mutex respectively to avoid conflict between different threads. The frequency table is implemented with the hist class we defined in Assignment 1.

