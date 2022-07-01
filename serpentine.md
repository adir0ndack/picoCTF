# Serpentine

**Description:** Find the flag in the Python script!



Use `wget` to download the given python script, and run it.

```bash
python3 serpentine.py
```

Notice that when you choose the option to print the flag, you are nudged to view the source code.
Use a text editor to review the code, and notice the function `def print_flag()`.

Look for the section where the function should be:

```python
elif choice == 'b':
      print('\nOops! I must have misplaced the print_flag function! Check my source code!\n\n')
```

Replace the print line by calling the function.

```python
elif choice == 'b':
      print_flag()
```

Run the script again, and choose option b to output the flag.
