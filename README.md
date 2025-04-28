# eBPF-PROJECT
# What is eBPF?

eBPF (Extended Berkeley Packet Filter) is a revolutionary technology originating from the Linux kernel. It allows sandboxed programs to run in privileged contexts such as the operating system kernel. These programs execute safely and efficiently without modifying the kernel source code or loading new kernel modules.

## Why eBPF?

Traditionally, the operating system kernel has been the ideal place to implement critical functionality such as:
- **Observability**
- **Security**
- **Networking**

This is because the kernel has privileged access and control over the entire system.

However, evolving the kernel is a complex and risky task. Due to its core role, kernel changes must ensure system stability and security, which slows down innovation at the OS level.

### eBPF solves this by:
- Allowing rapid innovation without kernel changes
- Enabling safe, high-performance extensions to the kernel
- Maintaining system stability and security

eBPF effectively extends the capabilities of the operating system in a secure and efficient manner.

## Why the Operating System Kernel?

Historically, the operating system has been the ideal place to implement observability, security, and networking functionality. This is because the kernel has a privileged position—it can observe and control all aspects of the system.

However, the kernel is also one of the most complex and sensitive parts of the operating system. Changing it is challenging due to the need for:

- High stability
- Strong security guarantees

This has traditionally made OS-level innovation slower compared to functionality developed outside the kernel.

## How eBPF Helps

eBPF enables the addition of new capabilities directly into the kernel—without modifying its source code or compromising system stability. It allows safe, dynamic, and high-performance extensions to the kernel, accelerating innovation in key areas such as networking, security, and observability.
## How eBPF Changes the Game

eBPF fundamentally redefines how functionality is added to the operating system. It enables sandboxed programs to run safely within the kernel at runtime. This allows application developers to enhance operating system behavior dynamically, without modifying kernel code or loading new modules.

These eBPF programs are verified for safety and compiled just-in-time (JIT) for performance, offering execution speed comparable to native code. A built-in verification engine ensures these programs do not compromise kernel stability or security.

As a result, eBPF has sparked the development of a wide range of cutting-edge projects across domains like:

- Next-generation networking
- Deep observability and tracing
- Advanced runtime security

## Modern Use Cases of eBPF

eBPF powers a growing ecosystem of tools and use cases including:

- **High-performance networking** and **load balancing** in data centers and cloud-native environments
- **Fine-grained security observability** with minimal overhead
- **Application tracing** for performance analysis and debugging
- **Container runtime security** enforcement
- **Real-time monitoring and troubleshooting**

The possibilities with eBPF are limitless, and this is just the beginning of its transformative impact on the operating system landscape.
## Hook Overview

eBPF programs are event-driven — they are triggered when a specific hook point in the kernel or application is reached. These predefined hook points include:

- System calls
- Function entry and exit
- Kernel tracepoints
- Network packet events
- And many more

When these events occur, the attached eBPF program is executed within the kernel in a secure and efficient manner.

If a required hook does not exist, custom hook points can be created using:

- **kprobes**: Attach to any kernel function
- **uprobes**: Attach to user-space application functions

This gives developers fine-grained control over where and how they observe and interact with system behavior.

### 📊 Visual Representation

1. **eBPF Execution Pipeline**:
   - Event occurs → eBPF program gets triggered
   - Verified for safety
   - JIT compiled for performance
   - Executed securely in kernel context

2. **Hook Types**:
   - Syscall hooks from user applications
   - kprobes and tracepoints from the kernel
   - XDP/Traffic Control hooks for networking

This flexibility allows eBPF to observe and control system behavior at almost any level — from user apps to the kernel and networking layers.
# 🚀 Loader & Verification Architecture

1. Tumne pseudo-C eBPF likha → "trace karo jab `open()` syscall chale"
2. Compile kiya → bytecode bana
3. bpf() syscall ke through load kiya
4. Kernel verifier ne check kiya → OK diya
5. JIT ne fast native code banaya
6. Hook pe attach ho gaya
7. Jab bhi `open()` syscall trigger hoga → tumhara program chalega ✅









a. eBPF Programs and Maps

eBPF Programs wo chhote-chhote C code hote hain jo Linux kernel ke andar run hote hain bina kernel ko modify kiye.

Ye code specific “hook points” par run hota hai jaise file read/write, network packet receive/send, syscalls, etc.

eBPF Maps ek special memory structure hota hai jisme eBPF program apna data temporarily store karta hai.

Jaise agar aapko syscall ka count rakhna ho, to map mein counter increment hoga.

Maps ko userspace program se access bhi kiya ja sakta hai.


b. Hook Points

Ye wo jagah hain jahan aapka eBPF code attach hota hai. Bahut saare hook points hote hain:

Kprobes / Kretprobes – Kernel ke function call ke aage/baad attach hote hain.

Uprobes / Uretprobes – User space program ke functions pe attach karne ke liye.

Tracepoints – Predefined hooks hote hain kernel mein (jaise sys_enter, net_dev_xmit, etc.)

XDP (eXpress Data Path) – Extremely fast networking hooks for packet filtering.

TC (Traffic Control) – Network packet processing for ingress/egress at interface level.

Socket Filters – Jaise tcpdump, raw packets inspect karne ke liye.


c. eBPF Verifier

Ye kernel ka component hai jo ensure karta hai ki eBPF program safe ho.

Agar program infinite loop mein chala gaya ya memory galat access kari to system crash ho sakta tha.

Verifier ensure karta hai:

Program loop-free ho.

Memory access valid ho.

CPU registers ka sahi use ho raha ho.

d. Userspace vs Kernelspace

Kernelspace mein eBPF program run hota hai – ye high-performance dete hain kyunki ye directly OS ke andar kaam karte hain.

Userspace se hum ye program load, manage, aur map access kar sakte hain using tools like bpftool, bcc, ya libbpf.


e. libbpf & BPF CO-RE

libbpf: C library jo userspace se eBPF program load karne mein madad karti hai.

BPF CO-RE (Compile Once, Run Everywhere): Aap ek baar eBPF program compile karte ho aur ye har compatible kernel pe chalega bina modify kiye.

Ye kernel version specific dependency hata deta hai

2. Tools Used in eBPF – 
a. BCC (BPF Compiler Collection)

Python based toolkit hai.

Easy to use, beginners ke liye best.

Pre-built examples jaise execsnoop, opensnoop, tcpconnect etc.


b. bpftrace

High-level language hai scripting ke liye.

Similar to awk/sed syntax – easy to write tracing scripts.

Real-time observability ke liye best tool hai.


c. libbpf

C developers ke liye low-level control deta hai.

Production systems mein use hota hai (e.g., Cilium, Katran by Meta).


d. bpftool

Command-line tool hai.

eBPF program inspect, attach, detach, log check, map manage, sab kuch kar sakte ho.

Command example: bpftool prog show, bpftool map dump id 42

# Slab Allocator Simulation
## Why?

This slab allocator solves several key memory management problems in C/C++ programming:

- **Reduces memory fragmentation**: By allocating memory in fixed-size blocks (slabs), it minimizes fragmentation.
  
- **Improves allocation and deallocation efficiency**: The allocator uses separate lists for allocated and free objects, reducing overhead and speeding up allocation and deallocation.

- **Allows for better tracking of memory usage**: Slab allocators track the number of allocated and free objects, providing real-time insights into memory usage.

- **Optimizes small object allocations**: Particularly beneficial in systems programming or embedded systems where small, frequent allocations are common.

By using the slab allocator, developers can implement a more efficient memory management system, especially in environments where performance and memory usage are critical.
## What?
## Slab Allocator in Kernel Module

A **slab allocator** in kernel modules is a memory management system used by the kernel to efficiently allocate and deallocate memory for objects of fixed sizes. It organizes memory into pre-allocated blocks called **slabs**, which are subdivided into **caches** to store objects of a specific size. This method reduces fragmentation and improves the performance of memory operations in the kernel.

### Key Features:
- **Object Caching**: Memory is allocated in slabs, which are divided into caches that hold objects of a fixed size.
- **Minimized Fragmentation**: Reduces both internal and external fragmentation by allocating memory in fixed-size chunks.
- **Efficient Allocation/Deallocation**: Allocates objects quickly from the free list in a slab and reuses memory, reducing overhead.
- **Multiple Object Sizes**: Supports different object sizes through separate caches for each type of object.
- **Cache Reuse**: Slabs and caches are reused to optimize memory management and prevent wastage.
## How?
# Slab Allocator Simulation in C++

This C++ program simulates a **Slab Allocator**, a memory management technique used to efficiently allocate and deallocate memory blocks of fixed sizes. A **Slab Allocator** minimizes fragmentation by allocating memory in large chunks (called "slabs") and then allocating smaller objects from these slabs.

## Code Breakdown

### **Classes and Structures:**

1. **SlabAllocator**:
   The main class that implements the slab allocation logic. It manages memory allocation and deallocation for various object sizes by storing them in **slabs**.

2. **Slab**:
   A private structure within the `SlabAllocator` class. It contains:
   - `freeObjects`: A vector holding objects that have been deallocated and are available for reuse.
   - `allocatedObjects`: A vector holding currently allocated objects.

### **Key Methods in `SlabAllocator`:**

1. **`~SlabAllocator`** (Destructor):
   - Ensures proper cleanup of memory. When the `SlabAllocator` is destroyed, it deallocates any objects that were allocated within slabs, freeing the memory.

2. **`allocate`**:
   - Allocates memory for an object of a specified size. If no slab exists for that size, it creates a new slab. If there are free objects in the slab, it reuses one of them; otherwise, it allocates a new block of memory.

3. **`deallocate`**:
   - Frees an object. It checks if the object is part of a slab. If it is, it moves the object from the allocated list to the free list. If not, an error message is printed, and the object is deleted.

4. **`printStatus`**:
   - Prints the current status of the slab for a specific object size: how many objects are allocated, how many are free, and provides a brief explanation of the slab allocator's functionality.

5. **`simulateMemoryOps`**:
   - Simulates a memory allocation and deallocation operation. It first allocates an object, then deallocates it, and prints the status of the slab after these operations.

6. **`printErrorTheory`**:
   - Prints an explanation for common errors, such as attempting to deallocate an object not managed by the allocator.

### **Menu and User Interaction (Main Function):**

1. **Menu**:
   The program provides a simple menu that allows users to interact with the `SlabAllocator`. Users can choose to allocate/deallocate objects, print the status of a slab, simulate memory operations, or exit the program.

2. **User Choices**:
   - **Allocate Object**: Allocates an object of a specified size and stores it in the slab allocator.
   - **Deallocate Object**: Frees an allocated object.
   - **Print Status**: Prints the current status of the slab (number of allocated/free objects).
   - **Simulate Memory Operations**: Simulates both allocation and deallocation of an object, then prints the slab status.
   - **Exit**: Exits the program.

### **Color and Formatting**:
The program uses **ANSI Escape Codes** to add colors and styles (e.g., red, green, yellow, bold, blue) to the console output. This enhances the clarity and visual appeal of different messages and warnings.

### **Flow of Execution**:

1. The user specifies the object size.
2. The program enters a loop where the user can choose operations like allocating or deallocating objects, checking the status of the allocator, or simulating memory operations.
3. When objects are allocated or deallocated, the program updates the state of the slabs, tracking which objects are free and which are in use.

### **Key Concepts Explained in the Code**:
- **Slab Allocation**: The program simulates how a slab allocator manages memory for objects of fixed sizes. Slabs help reduce memory fragmentation by reusing memory chunks.
- **Memory Operations**: The allocation and deallocation processes are modeled similarly to how memory is managed in operating system kernels.
- **Error Handling**: The program provides error messages when something goes wrong, such as trying to deallocate a non-existent object.

### **Summary**:
This program simulates a kernel-like memory management system using a **Slab Allocator**. It allows for efficient memory allocation and deallocation for objects of a fixed size. The program includes the ability to print status, simulate memory operations, and handle errors, making it a useful tool for understanding memory management techniques.
# Slab Allocator Simulation in C++

## Learning Outcomes

By the end of this project, the learner will be able to:

1. **Understand the concept of memory allocation and deallocation**: Gain an understanding of how memory is managed in systems, particularly using slab allocators.
2. **Implement a memory management system**: Learn how to create and manage a slab allocator, implementing memory allocation and deallocation methods in C++.
3. **Simulate kernel-level memory management**: Get hands-on experience with simulating how memory management works in the kernel, including tracking allocated and free memory blocks.
4. **Handle errors in memory management**: Learn to identify and handle errors in memory operations (e.g., deallocating objects not managed by the allocator).
5. **Work with dynamic memory in C++**: Develop an understanding of how to dynamically allocate and free memory in C++, as well as how to manage that memory in a structured way (using slabs).
6. **Improve debugging skills**: Through the use of status reports, error messages, and printouts, gain practice in debugging and troubleshooting memory management issues.
7. **Learn memory efficiency techniques**: Understand how techniques like slab allocation can reduce memory fragmentation and improve performance in systems.

## Why We Chose This Project?

As students, we chose to implement a **Slab Allocator Simulation** for several key reasons:

1. **Real-World Application**: Slab allocators are a fundamental concept used in operating systems and kernel memory management. Understanding how to allocate and deallocate memory efficiently is crucial for optimizing system performance and avoiding fragmentation.
   
2. **Enhancing Problem-Solving Skills**: This project helps develop problem-solving abilities by simulating complex memory management processes. It allows us to think critically about efficient memory usage, allocation strategies, and error handling.

3. **Hands-On Learning**: While studying memory management in theory, it’s essential to gain hands-on experience. Implementing a slab allocator in C++ provided an opportunity to directly apply what we've learned about dynamic memory management and object allocation in programming languages.

4. **Understanding C++ Memory Management**: This project deepened our understanding of **dynamic memory allocation** and the challenges associated with memory management in C++. By managing memory manually (with functions like `new` and `delete`), we were able to better appreciate memory leaks, fragmentation, and how systems like the kernel handle memory efficiently.

5. **Exposure to System-Level Programming**: Implementing a slab allocator allowed us to experience **system-level programming** concepts, which are often not fully covered in high-level languages or beginner courses. This gave us insight into how low-level memory operations are performed in real-time by operating systems.

6. **Simulating Real-World Systems**: Through the project, we simulated a critical system-level memory allocator. This experience allowed us to understand the importance of memory efficiency and how well-designed memory allocators contribute to a system’s overall stability and performance.

7. **Error Handling and Debugging**: We learned how to gracefully handle errors in memory management, including handling cases where objects are incorrectly deallocated or not tracked. This was an important learning experience in both memory management and debugging.

8. **Collaborative and Independent Work**: Although we worked individually on the project, it encouraged collaboration by discussing theoretical aspects of memory management with peers and seeking guidance from mentors. At the same time, it required us to independently think critically and implement a system that mimicked real-world memory management techniques.

In conclusion, this project allowed us to explore **critical thinking**, **memory efficiency**, and **system-level programming**, making it a valuable learning experience for anyone interested in systems programming, computer science, or software engineering.

## Project Summary

This project simulates a **Slab Allocator**, a memory management technique used to efficiently allocate and deallocate memory for objects of fixed sizes. The program is written in C++ and includes functionality for allocating and deallocating memory, printing slab status, simulating memory operations, and providing feedback for error handling. By simulating how slab allocators work in real-world systems, this project helps to better understand memory management and its critical role in preventing fragmentation and optimizing memory usage in operating systems.
