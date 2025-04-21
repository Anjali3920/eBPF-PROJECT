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

