## the `show_tree` method

`show_tree` is a convenience function for visualizing - at your terminal or IDE output - your un-expired pipeline files.  It is designed as a simple analog to the standard unix [tree command](https://www.tecmint.com/linux-tree-command-examples/).

To illustrate its usage we first process several files.

A table of contents for the remainder of this document is shown below.

- [basic pipeline setup](#basic-pipeline-setup)
- [basic usage, required input, and output breakdown](#basic-usage-required-input-and-output-breakdown)

## Basic pipeline setup

For this document we will use a pipeline consisting of a single [`parser` module](modules/parser.md).  We use [`create_pipeline`](system/create_save_load.md) to instantiate the pipeline.


```python
# create a pipeline with a single module
pipeline = krixik.create_pipeline(name="system-show-tree-docs",
                                  module_chain=["parser"])
```

## Basic usage, required input, and output breakdown

To illustrate the usage of `show_tree` we process a short file illustrated in the introduction to the [`parser` method](modules/parser.md#basic-usage-and-output-breakdown) - using various different metadata including `file_name`'s and `symbolic_directory_path`'s to illustrate the `show_tree` method.


```python
# define path to an input file from examples directory
test_file = "../../data/input/1984_very_short.txt"

# process short input file with various metdata
process_output = pipeline.process(local_file_path = test_file,
                                  local_save_directory="../../data/output", # save output repo data output subdir
                                  expire_time=60 * 10,      # set all process data to expire in 10 minutes
                                  wait_for_process=True,    # wait for process to complete before regaining ide
                                  verbose=False,
                                  symbolic_directory_path="/my/custom/path",
                                  file_name="file_num_one.txt")   

process_output = pipeline.process(local_file_path = test_file,
                                  local_save_directory="../../data/output", # save output repo data output subdir
                                  expire_time=60 * 10,      # set all process data to expire in 10 minutes
                                  wait_for_process=True,    # wait for process to complete before regaining ide
                                  verbose=False,
                                  symbolic_directory_path="/my/custom/path",
                                  file_name="file_num_two.txt")   

process_output = pipeline.process(local_file_path = test_file,
                                  local_save_directory="../../data/output", # save output repo data output subdir
                                  expire_time=60 * 10,      # set all process data to expire in 10 minutes
                                  wait_for_process=True,    # wait for process to complete before regaining ide
                                  verbose=False,
                                  symbolic_directory_path="/my/custom/path/subpath",
                                  file_name="file_num_three.txt")   
```

Now we can visualize our pipeline process file directory structure using `show_tree`.

`show_tree` takes in a single argument - `symbolic_directory_path`.  You can enter a path or stump (path + wildcard) to see all files and directories at or below the input path.


```python
# show the directory structure of a pipeline process file directory
show_tree_output = pipeline.show_tree(symbolic_directory_path='/*')
```

    /
    └── /my
        └── /custom
            └── /path
                ├── file_num_one.txt
                ├── file_num_two.txt
                └── /subpath
                    └── file_num_three.txt
