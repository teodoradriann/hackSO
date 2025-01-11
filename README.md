# Lambda Function Loader

## Team composition:

- Miron Adrian 324CC
- Barbu Alexandru 324CC

## Github:

- [original repo](https://github.com/teodoradriann/hackSO)

- [clean repo](https://github.com/teodoradriann/hackSO)

## Implementation details:

> NOTE: No extra functionality was implemented!

### `ipc.c` file

1. Socket Creation:
    - Function: create_socket
    - Creates a socket for Unix Domain communication using the AF_UNIX address family and SOCK_STREAM type.

2. Socket Connection:
    - Function: connect_socket
    - Connects a socket to a predefined server address (SOCKET_NAME).

3. Data Transmission:
    - Function: send_socket
    - Sends data reliably in chunks until the entire buffer is transmitted.

4. Data Reception:
    - Function: recv_socket
    - Receives data from a connected socket with built-in error handling.

5. Socket Closure:
    - Function: close_socket
    - Closes the socket safely with error reporting.

6. Error Handling:
    - Function: guard_let
    - Wraps system calls to detect and handle errors by printing a meaningful message and exiting the program when necessary.

### `server.c` file

1. Dynamic Library Loading and Execution
    - `lib_prehooks`: Prepares temporary files for library output and opens the library with dlopen.
    - `lib_load`: Dynamically loads a function (default is run) from the shared library using dlsym.
    - `lib_execute`: Redirects the program's stdout to a temporary file and executes the loaded function.
    - `lib_close`: Safely unloads the library using dlclose.
    - `lib_posthooks`: Validates post-execution output.

2. Unix Domain Socket Communication
    - Server Setup:
        - Creates and binds a Unix Domain Socket (SOCKET_NAME).
        - Listens for incoming client connections.
    
    - Client Interaction:
        - Receives commands from the client, parses them, and dynamically loads and executes the specified library function.
        - Sends back the result or error output to the client.

3. Command Parsing
    - `parse_command`: Parses the received client command into:
        - Library name
        - Function name
        - Function parameters

4. Error Handling
    - Robust error checking for system calls (socket, bind, listen, accept, etc.) and dynamic library operations (dlopen, dlsym).

5. Output Management
    - Redirects the library function's output to a temporary file using dup2 and returns the result to the client.

> NOTE: Client sends information to server like so:
bash
    <library_name> <function_name> <function_parameters>


## Extra features:

None.

## Info extra features:

None, we do not have extra features.

## How to test extra features:

N/A, we do not have extra features.
