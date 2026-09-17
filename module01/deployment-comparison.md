The customer support system must be accessible from outside the building because employees may need to work with customer tickets remotely. The system must remain available overnight so that support information can be accessed outside normal business hours. I expect medium growth as the business gains customers and employees. Employees do not need physical access to the server hardware. The business can afford a maximum of $100 per month for this workload.

## Deployment Comparison

### 1. VirtualBox on a Laptop

**What works:** VirtualBox provides a low-cost way to run the ticketing system in a virtual machine using hardware the business may already own. It is also useful for testing and learning because the virtual machine can be managed separately from the laptop's main operating system.

**What breaks:** The workload depends on one laptop remaining powered on and connected to the network. This makes reliable overnight availability and outside access more difficult. A laptop also provides limited room for growth compared with dedicated infrastructure.

### 2. Hyper-V on a Workstation

**What works:** Hyper-V can run the ticketing system as a virtual machine on a Windows workstation and provides better separation between the host computer and the server workload. It can make good use of existing business hardware.

**What breaks:** The service still depends on a single workstation and the business's local power and Internet connection. Hardware failure or maintenance on the workstation could make the ticketing system unavailable.

### 3. Proxmox Host

**What works:** Proxmox provides a dedicated virtualization environment that can host the ticketing system and additional virtual machines as the company grows. It provides more flexibility for managing server workloads than running the system on an employee laptop.

**What breaks:** The business must purchase or maintain suitable local server hardware. It is also responsible for power, networking, backups, updates, and hardware failures. Reliable external access requires additional network configuration.

### 4. Physical PC

**What works:** A dedicated physical PC gives the business direct control over the workload and avoids sharing resources with other virtual machines. The business owns and controls the hardware.

**What breaks:** The system is tied directly to one physical computer. Hardware failure could cause downtime, and increasing capacity may require purchasing or replacing components. The company would also be responsible for keeping the machine powered, connected, secured, and maintained.

### 5. Microsoft Azure

**What works:** Azure can make the ticketing system available over the Internet without requiring employees to physically access server hardware. Cloud resources can also be adjusted as the business grows, which supports the medium-growth requirement.

**What breaks:** Azure introduces an ongoing operating cost, and the business must monitor resource usage to remain within the $100 monthly budget. The company also depends on its Internet connection to manage and use the cloud-hosted workload.
## Recommendation

I would choose Microsoft Azure for the customer support and ticketing system. The deciding requirement for my choice is **overnight availability**. The business needs the ticketing system to remain available outside normal working hours, and I do not want its availability to depend on an employee laptop, workstation, or physical PC staying powered on at the office. Azure allows the workload to run in cloud infrastructure while still supporting external access and future growth. The business would need to monitor its Azure configuration and usage carefully to keep the workload within the $100 monthly budget.
