# The ALX Project: Unittests and Integration Tests
-------------

This project focuses on testing the functionalities of the __Github Organization Client__, 
using both __unit tests__ and __integration tests__. 

`Unit testing` validates specific functions for diverse inputs, ensuring expected outputs. 
It assesses standard and edge cases, focusing solely on the function's internal logic. 
__External function calls__, especially network or database operations, are typically __simulated__(__mocked__). 
The goal is to confirm if the function performs correctly within its defined scope, 
regardless of external factors.

`Integration tests` validate end-to-end code paths. 
They mock low-level functions involving external operations like __HTTP requests__ 
or file/database interactions. These tests examine interactions across the entire codebase, 
ensuring seamless integration between components.
 
Both tests are executed with:

```
python -m unittest path/to/test_file.py

```
Here's a comprehensive guide on how the tests are structured and executed:

## Unit Testing

__Access Nested Map Functionality__

The `utils.access_nested_map` function allows accessing deeply nested values 
within a mapping data structure. To ensure its correctness, `unit tests` have been created. 

__TestAccessNestedMap Class__:

`test_access_nested_map`: This method tests the access_nested_map function for standard inputs 
and corner cases. It uses the `@parameterized.expand decorator` 
to test the function with various inputs, ensuring the correct retrieval of nested values.
For instance: 

```
def test_access_nested_map(self):
    # Test with a nested map containing a single key
    nested_map = {"a": 1}
    path = ("a",)
    self.assertEqual(access_nested_map(nested_map, path), 1)

    # Test with a nested map containing multiple keys
    nested_map = {"a": {"b": 2}}
    path = ("a",)
    self.assertEqual(access_nested_map(nested_map, path), {"b": 2})

    # Test with a nested map and a multi-level path
    nested_map = {"a": {"b": 2}}
    path = ("a", "b")
    self.assertEqual(access_nested_map(nested_map, path), 2)

```


__Test 1: Nested Map with Single Key__:

In this test case, `nested_map` is a dictionary with a single key "a" 
whose corresponding value is `1`. The path variable represents the 
key path to access the value. The `access_nested_map` function 
is expected to `return 1` when given the path ("a",) for this scenario.

__Test 2: Nested Map with Multiple Keys__:

Here, nested_map is a dictionary containing a nested dictionary under the key "a". 
The function is tested with the path ("a",), and the expected result is {"b": 2}, 
indicating that the function should return the inner dictionary associated with the key "a".

__Test 3: Nested Map and Multi-Level Path__:

In this test case, nested_map is similar to the previous case, 
but the path now includes two keys: ("a", "b"). The function is expected to return 2, 
which is the value associated with the innermost key "b" within the nested dictionary.

__Assertions__:

```
self.assertEqual(actual_value, expected_value)

```

The assertEqual method is used to check if the access_nested_map function's output 
matches the expected results for each test scenario. If the actual value returned by access_nested_map 
matches the expected value, the test case passes. If not, the test would fail, i
ndicating a mismatch between expected and actual outcomes.

These test cases verify the correctness of the access_nested_map function for different 
input scenarios, ensuring it properly navigates nested dictionaries 
and retrieves the expected values based on the provided paths.

`test_access_nested_map_exception`: This method checks that a KeyError is raised 
when trying to access non-existing keys within the nested map. 
The decorator __@parameterized.expand__ is used to test different scenarios.
For instance: 

```
def test_access_nested_map_exception(self):
    # Test when the nested map is empty
    nested_map = {}
    path = ("a",)
    with self.assertRaises(KeyError) as context:
        access_nested_map(nested_map, path)
    self.assertEqual(str(context.exception), "'a'")

    # Test when a non-existing key is accessed within the nested map
    nested_map = {"a": 1}
    path = ("a", "b")
    with self.assertRaises(KeyError) as context:
        access_nested_map(nested_map, path)
    self.assertEqual(str(context.exception), "'b'")

```
