# SESSION 10 : Evolution from On-Premise Servers to Microservices :

## 1. On-Premise Servers :

- **Description**: Traditional model where servers and infrastructure are managed in-house.
- **Characteristics**:
  - **Hardware**: Physical servers located on-premises.
  - **Maintenance**: Managed by internal IT teams.
  - **Scalability**: Limited by physical capacity; requires hardware upgrades for scaling.
  - **Cost**: High initial investment in hardware and infrastructure.

## 2. Virtualization :

- **Description**: Introduction of virtual machines to optimize hardware utilization.
- **Characteristics**:
  - **Hardware**: Virtual servers on top of physical hardware.
  - **Maintenance**: Still managed internally but with improved resource allocation.
  - **Scalability**: Easier to scale compared to physical servers.
  - **Cost**: Reduced hardware costs due to better resource utilization.

## 3. Cloud Computing :

- **Description**: Utilizes cloud providers to deliver computing resources over the internet.
- **Characteristics**:
  - **Hardware**: Managed by cloud providers (e.g., AWS, Azure).
  - **Maintenance**: Minimal internal management; cloud provider handles infrastructure.
  - **Scalability**: On-demand scaling; pay-as-you-go model.
  - **Cost**: Variable cost based on usage; no upfront hardware investment.

## 4. Containers :

- **Description**: Lightweight, portable units that package applications and dependencies.
- **Characteristics**:
  - **Hardware**: Runs on shared operating systems.
  - **Maintenance**: Easier deployment and management compared to VMs.
  - **Scalability**: Fast scaling and deployment of applications.
  - **Cost**: Efficient use of resources; reduced overhead compared to VMs.

## 5. Microservices :

- **Description**: Architectural style where applications are composed of small, independent services.
- **Characteristics**:
  - **Hardware**: Typically deployed in cloud or containerized environments.
  - **Maintenance**: Decentralized; each service is managed independently.
  - **Scalability**: Fine-grained scaling of individual services.
  - **Cost**: Efficient use of resources; potentially lower costs with improved performance and scalability.

# Evolution from On-Premise Servers to Microservices :

|---------------------|
| **On-Premise Servers**  |
|---------------------|
          ↓           
|---------------------|
| **Virtualization**      |
|---------------------|
          ↓           
|---------------------|
| **Cloud Computing**     |
|---------------------|
          ↓           
|---------------------|
| **Containers**          |
|---------------------|
          ↓           
|---------------------|
| **Microservices**       |
|---------------------|

## 1. On-Premise Servers

| **Component** | **Role** |
|---------------|----------|
| **Hardware**  | Physical servers located on-premises. |
| **OS**        | Manages hardware resources and provides services to applications. |
| **Applications** | Software running directly on the OS, utilizing hardware resources. |
| **VM**        | Not used in this stage. |
| **Hypervisor** | Not used in this stage. |

## 2. Virtualization

| **Component** | **Role** |
|---------------|----------|
| **Hardware**  | Physical servers on which virtual machines are run. |
| **Hypervisor** | Software that creates and manages virtual machines on the hardware. |
| **VM**        | A virtual instance of a computer, running an OS and applications as if it were a physical machine. |
| **OS**        | Operating system running inside the VM, managing virtual resources. |
| **Applications** | Software running within the VM, utilizing the virtualized OS and resources. |

## 3. Cloud Computing

| **Component** | **Role** |
|---------------|----------|
| **Hardware**  | Managed by cloud providers; not directly handled by users. |
| **Hypervisor** | Used by cloud providers to manage virtual machines. |
| **VM**        | Used in cloud computing, but managed by the cloud provider. |
| **OS**        | Managed within the cloud infrastructure. |
| **Applications** | Applications hosted on cloud infrastructure, scaling as needed. |

## 4. Containers

| **Component** | **Role** |
|---------------|----------|
| **Hardware**  | Typically managed by cloud or container orchestration platforms. |
| **Hypervisor** | Not directly used; containers run on top of the host OS. |
| **VM**        | Optional; containers can run inside VMs or directly on the host OS. |
| **OS**        | Manages containers; often a shared OS across containers. |
| **Applications** | Software packaged within containers for consistent deployment. |

## 5. Microservices

| **Component** | **Role** |
|---------------|----------|
| **Hardware**  | Typically managed by cloud or container orchestration platforms. |
| **Hypervisor** | Not directly used; microservices run on containerized or serverless environments. |
| **VM**        | Optional; microservices can run inside VMs or directly in containers. |
| **OS**        | Managed within the containerized or serverless environment. |
| **Applications** | Small, independent services that work together to form a complete application. |
| **API**       | Interfaces through which microservices communicate with each other. |
| **Containers**| Often used to deploy microservices, allowing for isolation and scalability. |
| **Orchestration** | Tools like Kubernetes that manage the deployment and scaling of microservices. |


## Containers :

**Definition**: Containers are lightweight, portable units that bundle an application and all its dependencies (code, runtime, system tools, libraries, and settings) into a single package. They ensure that an application runs consistently across different computing environments.

### Key Characteristics:
- **Isolation**: Containers provide a way to run applications in isolated environments, preventing conflicts between them.
- **Portability**: Since containers package everything needed to run an application, they can be easily moved between different systems and environments.
- **Efficiency**: Containers share the host operating system’s kernel, making them more resource-efficient than virtual machines.
- **Scalability**: Containers can be quickly started and stopped, allowing applications to scale up or down as needed.

### Common Use Cases:
- **Application Deployment**: Containers make it easy to deploy applications consistently across development, testing, and production environments.
- **Microservices**: Containers are used to deploy individual microservices in a microservices architecture, enabling independent management and scaling.
- **Development and Testing**: Developers use containers to create isolated environments for consistent development and testing.

> Containers simplify application deployment and management, especially when used with tools like Kubernetes for orchestration.

## Containers :

| **Component** | **Role** |
|---------------|----------|
| **Hardware**  | Typically managed by cloud or container orchestration platforms. Users don't directly interact with physical servers. |
| **Hypervisor** | Not directly used; containers run on top of the host OS without needing a hypervisor. |
| **VM**        | A single virtual machine (VM) can be used to deploy many containers, with the hardware resources allocated from the VM. |
| **OS**        | Containers use a single operating system on the host. A small, lightweight operating system (like Alpine Linux) is often used within the container. |
| **Binaries/Libraries (Environment)** | Containers include all necessary binaries and libraries to run the applications, ensuring a consistent environment. |
| **Applications** | Software packaged within containers for consistent deployment across different environments. |

# Docker Hub :

**Definition**: Docker Hub is a cloud-based registry service provided by Docker that allows users to store, share, and manage Docker images. It is the default registry for Docker and provides a centralized place for image distribution and management.

## Components :

- **Item + Item = Repository**: A repository on Docker Hub is a collection of Docker images. Each repository can store different versions of an image, tagged with version names or other identifiers. Repositories help organize and manage Docker images for different applications or services.

- **Repository + Repository = Docker Hub**: Docker Hub is a service that hosts multiple repositories. It serves as a central registry where users can publish their Docker images, access images published by others, and collaborate on shared images.

- **SQL + Configuration + Start Script = Container**: A container includes everything needed to run an application, combining:
  - **SQL**: Database configurations or initialization scripts.
  - **Configuration**: Application configuration files and environment settings.
  - **Start Script**: Scripts that automate the startup process of the application within the container.

## Uses :

| **Use**                  | **Description** |
|--------------------------|-----------------|
| **Image Storage**        | Centralized location to store Docker images, making them easy to manage and retrieve. |
| **Image Sharing**        | Share Docker images with others by pushing them to Docker Hub repositories, facilitating collaboration. |
| **Version Management**   | Manage and deploy different versions of an application using tagged images. |
| **Automated Builds**     | Automate the building of Docker images from source code repositories, supporting continuous integration and delivery. |
| **Search and Discovery** | Search for and discover popular Docker images and repositories, making it easier to find pre-built images for various software. |
| **Access Control**       | Manage who can view or modify images by controlling access to repositories. |

