# 2. Create A New Token Project

## Create the project

To create a new project, we use the command `leo new <project_name>`

1. **Navigate to the Root Folder**
   - Ensure you are in the root folder of this `aleo-workshop` repository when you are creating a new project. (You must include your code in the repository for it to be considered finished.)
2. **Create a New Token Project**
   - In this example, we will create a new token project with a random name:

```bash
leo new token_$RANDOM
```

2.  You can also create the token with your custom name

```bash
leo new token_custom_name
```

2. Make sure everything is in lower case!

## Commands to run and test the project

1. **Enter the Project Directory:** After creating the project, navigate to the project directory:

```bash
cd token_<your_project_name>
```

2. **Build and Run the Program**: To build and run the program in `main.leo`, use the following command:

```bash
leo run main 0u32 1u32 # build & setup & prove & verify

You output should be:

Leo ✅ Compiled 'your_token_name.aleo' into Aleo instructions
⛓  Constraints
 •'your_token_name.aleo/main' - 33 constraints (called 1 time)
➡️  Output
 • 1u32
```

3. **Expected Output:**

```
Leo ✅ Compiled 'your_token_name' into Aleo instructions

⛓  Constraints

 • 'your_token_name.aleo/main' - 33 constraints (called 1 time)

➡️  Output

 • 1u32
```

4. You should see the output equal to `1u32`.

For more details about Aleo project interactions, check out [this guide](https://developer.aleo.org/leo/hello).

## Project Folder Outline

Here is an outline of the project folder structure:

```bash
.
├── README.md
├── build                   # Folder for all built `Aleo` files and manifest file.
│   ├── main.aleo           # `.Leo` file will be built into `.aleo`
│   └── program.json        # Program description file
├── program.json            # Program description file
├── src                     # Folder for all Program source codes
│   └── main.leo            # Define your program logic here
├── inputs                  # Folder for all input files
├── outputs                 # Folder for all output files
```
