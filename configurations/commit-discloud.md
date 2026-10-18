---
icon: code-commit
---

# Commit Discloud

## How to Correctly Create, Edit, and Replace Files Through Discloud Commits

When submitting commits through Discloud, it is essential to understand how the file submission process works and how the system determines which files should be created or updated.

The most important thing to understand is that **Discloud uses the paths and names of the submitted files to determine where files should be created or updated.** Therefore, if you want to replace an existing file, you must ensure that the submitted file matches the exact path of the original file.

A small mistake in a directory path, folder name, or even the capitalization of a single letter can cause a new file or directory to be created in a different location instead of replacing the original file.

This guide explains how the process works and what you must do to avoid these problems.

### 1. Understand How Commits Work in Discloud

When you submit a commit through Discloud, the system receives the submitted files and uses their paths to determine where they should be created or updated within your project.

There are two main scenarios:

* **Creating a file:** If the specified path does not contain a file with that name, the system may create a new file at that location.
* **Replacing an existing file:** If the specified path and filename exactly match those of an existing file, the system can update the original file with the new content.

This means that simply submitting a file with the same name is not enough to replace an existing file. You must also reproduce the entire directory structure leading to that file.

> **Discloud should not be treated as a system that automatically searches for a file by name and figures out which file you intended to replace. You must provide the correct path.**

### 2. Every Path Must Be Reproduced from the Project Root

Consider the following project structure:

```
my-bot/
├── package.json
├── index.js
└── src/
    └── commands/
        └── ping.js
```

In this example, `ping.js` is located inside the `commands` directory, which is itself inside the `src` directory.

Therefore, the complete relative path to the file is:

```
src/commands/ping.js
```

Now, imagine that you want to modify this file and submit the changes through a Discloud commit.

You must not place only `ping.js` at the root of the ZIP archive. You must also preserve the `src` and `commands` directories in their original hierarchy.

The ZIP file should reproduce the original structure:

```
update.zip
└── src/
    └── commands/
        └── ping.js
```

Notice that `ping.js` remains inside `commands`, and `commands` remains inside `src`.

This is essential because **Discloud uses the submitted paths relative to the project root to identify the files that should be created or updated.**

If the original file is inside one directory or several nested directories, you must reproduce every level of that structure in the ZIP file, preserving the original hierarchy.

### 3. Directory and Filename Matching Must Be Exact

This is one of the most important rules in the entire process.

When we say that names must be identical, we mean an exact match, including:

* Uppercase and lowercase letters.
* The complete name of every directory.
* The complete filename.
* File extensions, such as `.js`, `.ts`, `.json`, or `.py`.
* Special characters and any other characters in the original names.
* Every level of the directory hierarchy.

Suppose your original project contains this structure:

```
src/
└── commands/
    └── ping.js
```

The original directory is named `commands`, with all lowercase letters.

Now, imagine that you prepare your ZIP file with the following structure:

```
src/
└── Commands/
    └── ping.js
```

Notice the difference: the letter `C` in `Commands` is uppercase.

Although the names may look almost identical, they are different paths on the Linux filesystem used by Discloud.

The resulting structure could look like this:

```
project/
└── src/
    ├── commands/
    │   └── ping.js
    └── Commands/
        └── ping.js
```

Instead of replacing the original file, you may create a second directory inside `src`, containing another file named `ping.js`.

This happens because Linux treats `commands` and `Commands` as different directory names.

**Therefore, names must not merely look similar. They must match the original names exactly.**

### 4. Why Uppercase and Lowercase Letters Matter

Discloud runs on Linux-based infrastructure, and Linux filesystems normally distinguish between uppercase and lowercase letters.

This means that the following paths can represent different files or directories:

```
src/commands/ping.js
src/Commands/ping.js
src/COMMANDS/ping.js
```

The same applies to filenames:

```
config.json
Config.json
CONFIG.json
```

To a person, these names might appear to refer to the same file. To the operating system, however, they are different.

Consider the following example from a Node.js application:

```
const ping = require("./src/commands/ping.js");
```

This import statement looks for the file at `src/commands/ping.js`.

If you submit the file under `src/Commands/ping.js`, the import statement will still point to the original path. Node.js will not automatically search other directories for a file with the same name.

As a result, your bot may continue using the old file or encounter a module-not-found error, depending on the resulting project structure.

For this reason, preserving the original names is not simply an organizational preference. It is essential to ensure that your changes work as intended.

### 5. What Happens When You Submit an Incorrect Path?

Suppose you want to replace the following file:

```
src/commands/ping.js
```

However, when preparing the ZIP file, you accidentally create this structure:

```
src/Commands/ping.js
```

The file's content may be completely correct. The code may have been reviewed, all the intended changes may be present, and there may be no syntax errors.

Even so, the result may be incorrect because the file was submitted to the wrong location.

Instead of updating:

```
src/commands/ping.js
```

the system may create:

```
src/Commands/ping.js
```

You would then have two files with the same name in different directories.

This can lead to several problems:

* The bot continues executing the old version of the file.
* The submitted changes do not produce the expected result.
* Duplicate directories appear in the project.
* The code may encounter import errors.
* The project structure becomes inconsistent.
* Identifying and fixing future problems becomes more difficult.

The most dangerous part is that you may believe you updated the file successfully when, in reality, you only created a second version in a different location.

This is why checking file paths must be part of every Discloud commit workflow.

### 6. The ZIP Archive's Root Must Also Be Correct

In addition to preserving filenames and directory paths, you must verify how the files are organized inside the ZIP archive.

Suppose you want to update:

```
src/commands/ping.js
```

The expected structure would be:

```
update.zip
└── src/
    └── commands/
        └── ping.js
```

However, you might accidentally compress the entire project directory and produce this structure instead:

```
update.zip
└── my-bot/
    └── src/
        └── commands/
            └── ping.js
```

If Discloud processes the ZIP while preserving this outer directory, the resulting path could become:

```
project/
├── src/
│   └── commands/
│       └── ping.js
└── my-bot/
    └── src/
        └── commands/
            └── ping.js
```

In this case, you may have created an additional directory structure instead of updating the original file.

The exact result depends on how Discloud's commit mechanism processes ZIP archives. Therefore, you must verify whether the system expects files directly at the archive root or applies any specific extraction rules.

The practical rule is simple: **the directory structure inside the ZIP must match the relative paths expected by the commit mechanism, taking into account how Discloud processes submitted files.**

### 7. The Correct Procedure Before Submitting a Commit

To avoid errors, follow these steps whenever you need to create or replace files through Discloud.

**Step 1 — Locate the original file.**

Find the file you want to modify and identify the exact directory in which it is located.

**Step 2 — Identify the complete path.**

If the file is located at `src/commands/ping.js`, use that exact path as your reference.

**Step 3 — Reproduce the entire directory structure.**

Create the `src` and `commands` directories inside the ZIP file, preserving their original hierarchy.

**Step 4 — Verify every name.**

Check that every directory and filename matches the original project exactly, including uppercase and lowercase letters.

**Step 5 — Verify the file extension.**

If the original file is named `ping.js`, do not submit it as `Ping.js`, `ping.JS`, or `ping.js.txt`.

**Step 6 — Check the ZIP archive's root.**

Make sure you have not included an unnecessary outer directory that changes the expected destination path.

**Step 7 — Review the file content.**

Confirm that the submitted file contains the intended changes and is not incomplete.

**Step 8 — Verify the commit result.**

Whenever possible, inspect the recorded changes and the resulting project structure. If you intended to replace a file but the result shows a newly created duplicate directory, investigate the issue before proceeding.

### 8. Complete Example: Submitting a Correct Commit

Imagine your bot has the following structure:

```
my-bot/
├── index.js
├── package.json
└── src/
    ├── commands/
    │   ├── ping.js
    │   └── help.js
    └── events/
        └── ready.js
```

You want to modify only `ping.js`.

If Discloud's commit mechanism supports partial file submissions, your ZIP archive can contain only the file you need to update:

```
update.zip
└── src/
    └── commands/
        └── ping.js
```

You do not need to include the other files if they are not being modified.

The expected destination path is:

```
src/commands/ping.js
```

After the change is applied correctly, the project structure should remain organized in the same way, with only the content of `ping.js` updated.

The files `index.js`, `package.json`, `help.js`, and `ready.js` should remain unchanged.

However, if you submit the file under `src/Commands/ping.js`, you may create a duplicate directory. If you include an outer `my-bot` directory when the commit mechanism does not expect it, you may also create an incorrect path.

The goal is to modify exactly the intended file without creating unnecessary copies or changing the rest of the project structure.

### 9. Rules You Must Follow for Every Commit

To maintain an organized project and avoid problems during updates, follow these rules:

1. **Preserve the complete path:** Reproduce every directory between the project root and the file you want to modify.
2. **Preserve capitalization:** `commands` and `Commands` are different names on Linux.
3. **Do not rename directories unnecessarily:** Keep the original directory and filename conventions.
4. **Do not submit only the filename when the file is inside a subdirectory:** Reproduce the required path.
5. **Avoid unnecessary directory levels:** Check that the ZIP does not contain an outer directory that changes the expected destination.
6. **Avoid submitting unnecessary files:** Keep each commit focused on the intended changes.
7. **Verify the result:** Confirm that the original file was updated and no duplicate directories were created.
8. **Do not assume Discloud will correct the paths:** Submit the correct structure from the beginning.

### 10. The Fundamental Rule: Path Accuracy

The most important principle is understanding that Discloud should not be treated as a system that automatically discovers which file you want to replace based only on its name.

If the original file is located at:

```
src/commands/ping.js
```

that is the path you must reproduce in your commit.

If you submit:

```
src/Commands/ping.js
```

you are specifying a different path.

If you submit:

```
my-bot/src/commands/ping.js
```

you may be introducing an unnecessary directory level.

And if you submit only:

```
ping.js
```

you may create or update a file at the project root instead of modifying the file you actually intended to change.

Therefore, before submitting any Discloud commit, always verify these three essential elements:

* **The complete file path.**
* **The exact spelling and capitalization of every directory.**
* **The exact filename and extension.**

These precautions are essential to ensure that changes are applied in the correct location, preventing duplicate files, inconsistent directories, and problems when running your bot.

The goal is not simply to submit a successful commit. It is to ensure that the commit produces the intended result, preserves the project's structure, and modifies exactly the files that need to be changed.

> **On Discloud, path accuracy is essential for maintaining project consistency. Before submitting a commit, verify the directory structure, validate every filename, and make sure each file is in the correct location.**
