# air_mouse
you can control mouse using your hand and camera

**Description:**

This Python code implements a gRPC server that calculates Fibonacci numbers. It allows clients to send requests for specific Fibonacci numbers, and the server computes and returns the corresponding value.

**Installation:**

The code assumes you have Python and the `grpcio` library installed. You can install `grpcio` using pip:

```bash
pip install grpcio
```

**Usage:**

1. **Save the Code:** Save the code as a Python file (e.g., `fib_calculator_server.py`).
2. **Run the Server:** Execute the script using the following command, specifying the desired IP address and port (default is 0.0.0.0 and 8080, respectively):

   ```bash
   python fib_calculator_server.py --ip [IP_ADDRESS] --port [PORT_NUMBER]
   ```

   Replace `[IP_ADDRESS]` with the IP address you want the server to listen on (0.0.0.0 for all interfaces) and `[PORT_NUMBER]` with the desired port number.

**Code Structure:**

The code is organized into several sections:

- **Imports:** Necessary libraries are imported, including `os`, `os.path`, `sys`, `argparse`, `grpc`, `concurrent.futures`, `fib_pb2`, and `fib_pb2_grpc`.
- **Constants:** The `BUILD_DIR` constant is defined using `os.path.join` to dynamically locate the directory containing the generated gRPC service definition files (assuming you've used the gRPC protocol buffer compiler). The path is then added to the system path using `sys.path.insert(0, BUILD_DIR)`.
- **`FibCalculatorServicer` Class:** This class inherits from the `fib_pb2_grpc.FibCalculatorServicer` class, implementing the gRPC service definition.
  - `__init__()`: The constructor is currently empty.
  - `Compute(self, request, context)`: This method is called when a client sends a request to calculate the Fibonacci number. It extracts the order (`n`) from the request message, calls the `_fibonacci` helper function to calculate the value, and constructs a response message with the calculated value.
  - `_fibonacci(self, n)`: This helper function implements the Fibonacci sequence logic using a loop to compute the `n`th Fibonacci number.
- **`if __name__ == "__main__":` Block:** This block executes only when the script is run directly (not imported as a module).
  - `argparse` is used to create an argument parser for handling command-line options. It defines options for `--ip` (IP address) and `--port` (port number).
  - The server is created using `grpc.server` with a thread pool executor for handling concurrent requests.
  - An instance of the `FibCalculatorServicer` class is created.
  - The service is added to the server using `fib_pb2_grpc.add_FibCalculatorServicer_to_server`.
  - An insecure port is added to the server using `server.add_insecure_port`.
  - The server is started with `server.start()`, and a message is printed indicating the server's IP and port.
  - The server waits for termination using `server.wait_for_termination()`.
  - A `try-except` block is used to gracefully handle keyboard interrupts (`KeyboardInterrupt`).

**Dependencies:**

- Python 3 (tested with 3.x)
- `grpcio` library

**Additional Notes:**

- This code demonstrates a basic gRPC server implementation. You might need to modify it for production use, such as handling authentication, error scenarios, and more robust logging.
- The `fib_pb2` and `fib_pb2_grpc` modules are likely generated from a protocol buffer definition file (`.proto` file). Ensure you have these modules available in your project structure.

I hope this detailed explanation is helpful!
