# Containers and Hypervisors

## Linux Virtualization

Why virutalization?

- security
- efficient hardware usage
- separation of concerns
- hardware independent

Non-Linux alternatives available, e.g l4re based.

### KVM & XEN - Linux Type 1 Hypervisors

Linux offers two different Type 1 Hypervisors, KVM and XEN.

#### KVM - Kernel-based Virtual Machine

- Supports Linux, Windows, BSD and Soliars as guest OS
- Supports virtualization extension of  x86 and x86-64 CPUs
- Released 2007
- Guest OS runs as a process can gets dedicated hardware (memory, disks, CPUs)

Pros:
- Excellent security based on SE Linux
- Open Source

Cons:
- Complex setup process
- Limited support if processors
- No built-in CPU virtualization

#### XEN

- Released 2003
- Support for Windows and Linux
- Support for IA-32, ARM and x86 processors
- First choice for hyper-scaled industrial clouds (Amazon, ...)
- Advanced security, good choice for security-related environments

Pros:
- Open Source
- Support for live migration of virtual machines
- Easy to use GUI
- Snapshot feature
- Support for moving between pysical servers
- Easy configuration
- Failure management support

Cons:
- Free version is limited
- No USB support
- Less technical support
- Less stable virtual networks
- Complex storage extension

#### Comparison of KVM and XEN

KVM:
- lightweight hypervisor module based on Linux Kernel
- requires hardware support (e.g. CPU with VT function)
- part of the Linux kernel
- small overhead / almost native performance

XEN:
- XEN runs on top if Linux
- Linux kernel with enabled XEN support needed
- external hypervisor
- small overhead / almost native perfomance

### Vagrant

- Tool for working with virtual environments
- Support for text-based environment definitions
- Additional simple layer on top of different hypervisors
- Supported backends: VirtualBox, KVM, Hyper-V, Docker, VMWare, ...

### QEMU - Quick Emulator

- Open Source emulator
- Binary translation of CPU instructions
- Virtual hardware
- Support for KVM (allowing almost native speed when emulating same CPU  architecture)
- Supported instruction sets: x86. MIPS, 32-bit ARMv7, ARMv8, PowerPC, SPARC, ETRAC CRIS, MicroBlaze
- QEMU can save and restore the state of a VM
- large overhead in case of binary translation

Operation modes:
- User-mode emulation: run single program compiled for a different instruction set (debugging)
- System emulation: emulate a full computer system including peripherals (virtualization or embedded Linux development)
- KVM hosting: QEMU setting up a KVM image. QEMU is emulating the hardware, KVM is executing the software
- XEN hosting: QEMU is only emulating the hardware, XEN has full control of execution

### OpenVZ

- Container solution, no virtualization or hypervisor
- Based on a patched Linux kernel
- All containers share a single kernel instance
- No performance overhead

## Containers

- Containers are operating-system-level virtualization
- Isolate applications form the host system
- Package applications and dependencies (support of different library versions per application, but duplication of libraries per application)
- Behave like virtual machines
- No duplication of the operating system, only one kernel for all containers, no performance overhead
- Based on Linux kernel features cgroups and namespaces
- No hardware support needed
- Drawbacks: More disk space needed (duplication of application dependencies) and amplification of updates (update of a shared library requires rebuild of all application containers using the library)

### cgroups - control groups

- Linux kernel feature to limit, account and isolate resource usage of processes
- Part of kernel since 2.6.24
- cgroups v2 is part of kernel since 4.5
- Goal of cgroups: unified interface for controlling processes (from nice to virtualization)
- Features: Resource limitation, priorization, accounting resouce usage, control of processes
- Usage: cgroup virtual file system or tools from libcgroup
- Indirect usage: Docker, LCX, libvirt, ...

### Linux namespaces

- Linux kernel feature to partition kernel resources (set of processes sees only a set of resources)
- Resources may exist in mutliple namespaces, examples of resoruces: PIDs, hostname, UIDs, file names, IPC
- Linux starts with a single namespace for all processes, processes can create additional namespaces and join different namespaces
- Part of kernel since 2.4.19
- Feature set needed for containers (user namespaces) since kernel 3.8

Kind of namespaces (since kernel 5.6):
- Mount (mnt): Mount namespaces control mount points. Mount namespaces are copied.
- Process ID (pid): PID namespaces provide and independent set of process IDs. PID namespaces are nested.
- Network (net): Network namespaces virtualize the network stack. On creation a network namespace contains only a loopback interface. Each network interface (physical or virtual) is present in exactly 1 namespace and cen be moved between namespaces.
- Interprocess Communication (ipc): IPC namespaces isolate processes form SysV style inter-process communication. This prevents processes in different IPC namespaces from using the SHM family of functions to establish a range of shared memory between the two processes.
- UTS (UNIX Time-Sharing): UTS namespaces allow a single system to appear to have different host and domain names.
- User ID (user): User namespaces are a feature to provide priviledge isolation and user identification segregation. Available since kernel 3.8.
- cgroup Namespace: The cgroup namespace type hides the identity of the control group of which a process is a member. Available since kernel 4.6.
- Time Namespace: The time namespace allows processes to see different system times. Available since kernel 5.6.

## LXC - Linux containers

- Operating-system-level virtualization
- Based on kernel features cgroups and namespaces
- Focus on full system containers
- Used by early versions of Docker (before 0.9, support dropped with 1.10)
- In kernels before 3.8: container root can run code with host root privileges (fixed with 1.0 if proper configured)
- Since 1.0: support for unpriviledged containers (run container as regular user)
- Lightweight C application, compared to runC

### LXD

- Container manager, alternative to LXC tools
- Build on top of LXC
- Improved user experience

## Open Container Initiative (OCI)

- OCI is a Linux Foundation project, started 2015 by Docker
- Specificaitons: Runtime Specificaiton and Image Specification

### runC

- runC is the reference implementation of the OCI runtime specification
- Written in Go
- First release v0.0.1 in 2015
- Basis of higher level tools, e.g. Docker

### crun

- OCI runtime implementation
- Written in C, focus on low-memory footprint
- Drop-in replacement for runC, feature compatible

## Container Runtime Interface (CRI)

- high-level spec describing a container runtime from container-orchestration perspective
- describes image management and distribution, storage, snapshotting and networking

## containerd

- Developed by Docker
- Full CRI implementation
- Container runtime available for Linux and Windows
- Manage the complete container lifecycle: image transfer and storage, container execution and supervision, low-level storage and network attachments
- Middleware used by Docker, Google Cloud Platform, AWS, Azure, ...
- Build on top of platform specific container runtimes, e.g. runC, runhcs, gVisor, ...
- Alternative: CRI-O

## Docker

- Set of open soure software and payed PaaS products
- OS-level virtualization with focus in app bundling (one process per container)
- Available for Linux, Windows, macOS
- Platforms: x86-64, ARM, s390x ppc64le
- Written in Go
- First release 2013
- Builds on containers and Linux and a shared virtual machine on other platforms
- Supports different container middleware on Linux, e.g. containerd, libvirt, LXC, systemd-nspawn
- Provides a high level APi, similar to Vagrant for vitual machines
- Supports also Windows containers

Components:

Software:
- Docker deamon (dockerd): service which manages the containers, provides Docker Engine API
- Docker client (docker): CLI to interact with dockerd

Objects:
- container: standardized, encapsulate environment that runs applications
- image: read-only tempate used to build containers

Registries: Repository for Docker images. Docker clients can download and upload/publish images

Aternative: Red Hat stack: crun (runtime), cri-o (CRI middleware), podman (docker service alternative), buildah (image building), skopeo (image distribution)

## Kubernets

- Open source container orchestration for automating software deployment
- Support Docker, Containerd and CRI-O
- Offered by many Cloud providers
- Released 2015
- Kubernetes Pod: Basic scheduling unit, consisting of one ore more containers

## Podman

- Developed by Red Hat
- Pod Manager tool
- Intended as Docker drop in replacment, similar CLI interace
- Middleware: libpod
- No service but Fork-Exec-Model, container becomes child process of podman
- rootless, i.e. container doesn't run with root privileges
- Compatible with systemd

## Systemd-nspawn

- Systemd component to run containers
- Supports OCI containers
-

## Container communication

- Primary container communication is (virtual) networking
- Bind-mounted file system can be used to share data between containers and the host
- /dev/shm can be used as "ram drive"
- Unix sockets created on a shared volume

## Flatpack - a application container solution

- Application sandbox
- Developed by freedesktop.org
- Inital release 2015
- Access to host system configured by permissions (similar to Android/iOS)
- Build on namespaces, cgroups
- Repos not linked to distributions
- Alternative: Snap (Caninical, partially closed source)

# References

## Virtualization

- https://vpntester.org/blog/unterschied-xen-openvz-kvm-virtualisierung-server/
- https://1gbits.com/blog/head-to-head-comparison-kvm-vs-xen/
- https://en.wikipedia.org/wiki/Xen
- https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine
- https://en.wikipedia.org/wiki/QEMU
- https://opensource.com/resources/vagrant
- https://en.wikipedia.org/wiki/Vagrant_(software]

## Containers

- https://opensource.com/resources/what-are-linux-containers
- https://www.redhat.com/en/topics/containers?extIdCarryOver=true&sc_cid=701f2000001OH79AAG
- https://en.wikipedia.org/wiki/Linux_namespaces
- https://en.wikipedia.org/wiki/Cgroups
- https://en.wikipedia.org/wiki/OS-level_virtualization#Implementations
- https://en.wikipedia.org/wiki/LXC
- https://www.section.io/engineering-education/lxc-vs-docker-what-is-the-difference-and-why-docker-is-better/
- https://en.wikipedia.org/wiki/Open_Container_Initiative
- https://github.com/containerd/containerd
- https://containerd.io/
- https://en.wikipedia.org/wiki/Docker_(software)
- https://www.kreyman.de/index.php/others/linux-kubernetes/232-unterschiede-zwischen-docker-containerd-cri-o-und-runc
- https://en.wikipedia.org/wiki/Kubernetes
- https://podman.io/
- https://www.heise.de/hintergrund/Podman-Linux-Container-einfach-gemacht-Teil-1-4329067.html
- https://www.vdz.org/digitalisierung-der-verwaltung/podman-vs-docker-was-bringt-die-zukunft-der-container-welt
- https://www.imaginarycloud.com/blog/podman-vs-docker/
- https://blog.selectel.com/systemd-containers-introduction-systemd-nspawn/
- https://medium.com/@huljar/setting-up-containers-with-systemd-nspawn-b719cff0fb8d
- https://www.phoronix.com/scan.php?page=news_item&px=Systemd-Nspawn-OCI-Runtime
- https://www.tutorialworks.com/container-networking/
- https://datawookie.dev/blog/2021/11/shared-memory-docker/#:~:text=The%20shared%20memory%20device%2C%20%2Fdev,%2Dprocess%20communication%20(IPC).
- https://www.digitalocean.com/community/tutorials/how-to-share-data-between-the-docker-container-and-the-host
- https://www.jujens.eu/posts/en/2017/Feb/15/docker-unix-socket/
- https://www.section.io/engineering-education/lxc-vs-docker-what-is-the-difference-and-why-docker-is-better/
- https://www.techdivision.com/aktuelles/blog/lxc-vs-docker-wir-setzen-bei-techdivision-inzwischen-verstaerkt-auf-lxc#:~:text=Um%20ein%20Image%20aus%20einem,Verzeichnis%20als%20tar%20hochgeladen%20werden.&text=Andererseits%20bietet%20Docker%20eine%20raffiniertere,mit%20der%20Speicherung%20eines%20Image.
- https://www.capitalone.com/tech/cloud/container-runtime/
- https://www.redhat.com/sysadmin/introduction-crun
- https://flatpak.org/faq/
- https://www.youtube.com/watch?v=sK5i-N34im8
