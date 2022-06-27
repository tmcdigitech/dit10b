---
title: "1: Programming Checkpoints"
---

{{< hint info >}}
[Hand in your files here](http://10.124.229.70:8080/).
{{< /hint >}}

You will need to save each of the tasks in this set in its own file, with a simple naming system:
- **1. Three in, three out** should be in a file named `ex1.py`,
- **2. Name swapper** should be in a file named `ex2.py`

and so on.

You will be submitting these files to a system which will mark them automatically.
Since they'll be marked by a computer, and computers are terminally stupid, you
will need to make sure that your files are labelled correctly, or the computer
will assume you haven't done that particular exercise. You will also need to
make sure your output exactly matches the examples, down to capitalisation,
spelling, line breaks and spaces.

## Structure of each file
Each file will need to have some code at the top and bottom to make it possible for
the marking system to check it.

Here is an example file for the second challenge, with the additional code highlighted:
{{< highlight python "linenos=table,hl_lines=1 8-9"  >}}
def main(input,print):
    print("What is your first name?")
    fname = input("> ")
    print("What is your sirname?")
    sname = input("> ")
    print(f"{sname} {fname}")

if __name__ == "__main__":
    main(input,print)
{{< /highlight >}}

Take particular note of the indentation.