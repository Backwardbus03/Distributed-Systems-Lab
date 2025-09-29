# Distributed Traffic Signal Controller (RPyC)

## Project Overview

This project implements a simulated distributed 4-way traffic intersection control system. It uses **RPyC (Remote Python Call)** for inter-process communication between a central server and multiple GUI clients.

The system features robust distributed systems concepts, including:
* Client registration and minimum connection requirements.
* Thread-safe state management.
* Request Queuing and Load Balancing (Task 4).
* Priority-based request handling for VIP vehicles (Task 3: Deadlock Management).
* Manual Override for RTO (Road Transport Office) clients (Task 5: Write).

***

## System Components

| Component | File | Description |
| :--- | :--- | :--- |
| **Traffic Controller Server** | `signal_controller_server_full.py` | The core RPyC service that runs the signal logic, state management, request queues, and handles client connections. |
| **Traffic Display Client** | `traffic_display_client.py` | A GUI that visualizes the 4-way intersection and traffic lights in real-time. |
| **Pedestrian Display Client** | `pedestrian_display_client.py` | A GUI that shows the current **WALK** / **STOP** state for the two pedestrian crossings. |
| **RTO Control Client** | `rto_client.py` | A GUI for monitoring signal status and providing manual override control to force a signal to GREEN. |

***

## Prerequisites

* **Python 3.x**
* **RPyC:** Install using `pip install rpyc`
* **Tkinter:** Usually included with standard Python distributions.

***

## How to Run the System

The server requires multiple clients to be registered before it begins the main control loop.

**Note:** All RPyC connections are configured with `'config={'allow_pickle': True}` to handle complex data structures being passed across the network.

### Step 1: Start the Server

Start the traffic controller on the desired host and port (defaults to `0.0.0.0:18812`) : python signal_controller_server_full.py

### Step 2: Start the Clients
Start the client applications. The server's main control loop will not begin until the minimum required clients are connected (1 traffic_display, 2 pedestrian_display in the server's default configuration).

- Start the main traffic visualization :
  - python traffic_display_client.py localhost 18812

* Start the pedestrian signal display (can run multiple instances) : 
  - python pedestrian_display_client.py localhost 18812
  - python pedestrian_display_client.py localhost 18812 # Second instance to meet requirement

- Start the RTO control panel :
  - python rto_client.py localhost 18812 (You can replace localhost and 18812 with the server's IP address and port if running on different machines.)

