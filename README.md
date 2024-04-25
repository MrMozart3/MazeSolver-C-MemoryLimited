# Maze Solver
##### C program for solving mazes. Quick and reliable. RAM usage doesnt exceed 100kB during runtime.
## Installation
Intallation on Ubuntu linux:
> Download files from repository

> $ make

> ./labsolver < parameters >

### Parameters
`-t <Mode>` (required)

| Mode | Description  |
| ---- |---- |
| 0   |  .txt input and .txt output |
| 1 |  binary input and binary output |
| 2 |  binary input and .txt output |

`-n <Input filename>` (required)
This file contains unsolved maze (binary or .txt)

`-o  <Output filename>` (required when t != 1)
Instructions how to solve maze will be printed to this file

`-s <chunkSize>` (optional)
Defines size of single chunk

`-c <cacheSize>` (optional)
Defines size of cache

`-r <recordSize>` (optional)
Defines size of single record in temporary file chunks.

`-d` (optional)
Runs program in debug mode

`-h`
Shows Help Message

## Files
Program accepts files in two types Binary and standard text file.
### 1. Binary File
##### Binary File can contain maze and solution at the same time. It has to follow this structure:
##### Header ( section 1 ):

| Name | Size in Bytes  | Description |
| ------------ | ------------ | ------------ |
| File ID | 4 | File ID: 0x52524243  |
| Escape | 1 | ESC: 0x1B |
| Columns | 2 | Maze Columns (starts from 1) |
| Lines | 2 | Maze Rows (starts from 1) |
| Entry X | 2 | Maze Entry X (starts from 1) |
| Entry Y | 2 | Maze Entry Y (starts from 1) |
| Exit X | 2 | Maze Exit X (starts from 1) |
| Exit Y | 2 | Maze Exit Y (starts from 1) |
| Reserved | 12 | Reserved for future usage |
| Counter | 4 | Number of blocks(section 2) |
| Reserved | 4 | Reserved for future usage |
| Separator | 1 | Begins new block |
| Wall | 1 | Value defines Wall of the maze |
| Path | 1 | Value defines Path of the maze |

##### Blocks ( section 2 ):
Each block in this section is defined like this:

| Name | Size in Bytes  | Description |
| ------------ | ------------ | ------------ |
| Separator | 1 | Begins new block |
| Value | 1 | Wall / Path |
| Count | 1 | Number of Values (0 means 1 occourance, 1 means 2...) |

> Number of blocks should match Counter in Header ( section 1 )

##### Solution Header ( section 3 ):

| Name | Size in Bytes  | Description |
| ------------ | ------------ | ------------ |
| File ID | 4 | File ID: 0x52524243  |
| Steps | 4 | Steps to solve maze (0 means 1 occourance, 1 means 2...) |

> Input File containing only maze (without solution) should end at File ID in section 3.
 
##### Solution Steps ( section 4 ):

| Name | Size in Bytes  | Description |
| ------------ | ------------ | ------------ |
| Direction | 1 | N / S / W / E  |
| Counter | 1 | Fields to go by |

### 2. Input Text File
##### This type of file should be formatted this way:

##### Where:
'X' - Wall

'P' - Entry

'K' - Exit

### 3. Output Text File
Output text file contains solved maze in steps (1 line = 1 step) :

![](https://raw.githubusercontent.com/MrMozart3/MazeSolver-C-MemoryLimited/e3dd943842fd146e9c72954516cc27c11294b3e7/example_maze.png)

##### Example:

>N 3
>
>E 1
>
>S 2
>
>W 3
