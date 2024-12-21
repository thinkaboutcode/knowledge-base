# Overview of Network Layers

The network layers refer to the **layers of the OSI model** (Open Systems Interconnection model), a conceptual framework used to standardize networking protocols and facilitate communication across diverse systems. The model comprises **seven layers**, each responsible for specific functions in the data communication process.

---

## 1. Physical Layer
- **Function**: Handles the physical connection between devices, transmitting raw bits over a physical medium.
- **Key Responsibilities**:
    - Signal transmission (electrical, optical, radio)
    - Connector and cable specifications
    - Bit synchronization
    - Data encoding and modulation
- **Devices**: Cables, switches (layer 1), hubs, repeaters.

---

## 2. Data Link Layer
- **Function**: Ensures reliable data transfer across a physical link by detecting and correcting errors.
- **Key Responsibilities**:
    - Framing (dividing data into manageable chunks)
    - MAC (Media Access Control) addressing
    - Error detection and correction (e.g., CRC)
    - Flow control
- **Protocols**: Ethernet, Wi-Fi (IEEE 802.11), PPP (Point-to-Point Protocol).
- **Devices**: Layer 2 switches, bridges.

---

## 3. Network Layer
- **Function**: Handles routing, addressing, and forwarding of data packets across different networks.
- **Key Responsibilities**:
    - Logical addressing (e.g., IP addresses)
    - Path determination and routing
    - Packet forwarding
- **Protocols**: IP (IPv4/IPv6), ICMP, ARP.
- **Devices**: Routers, layer 3 switches.

---

## 4. Transport Layer
- **Function**: Provides end-to-end communication, ensuring reliable or connectionless delivery of data.
- **Key Responsibilities**:
    - Segmentation and reassembly of data
    - Connection establishment and termination
    - Flow control and congestion control
    - Error detection and recovery
- **Protocols**: TCP (Transmission Control Protocol), UDP (User Datagram Protocol).

---

## 5. Session Layer
- **Function**: Manages and controls the dialog between two systems (establishing, maintaining, and terminating connections).
- **Key Responsibilities**:
    - Session establishment, maintenance, and termination
    - Synchronization and checkpointing
- **Protocols**: NetBIOS, RPC (Remote Procedure Call).

---

## 6. Presentation Layer
- **Function**: Translates data between the application and network format, ensuring proper interpretation of transmitted data.
- **Key Responsibilities**:
    - Data encryption and decryption
    - Data compression
    - Data format translation (e.g., ASCII to EBCDIC)
- **Protocols**: SSL/TLS, JPEG, GIF, MPEG.

---

## 7. Application Layer
- **Function**: Provides the interface for the user or application to access network services.
- **Key Responsibilities**:
    - Application services (e.g., file transfer, email, web browsing)
    - Resource sharing
- **Protocols**: HTTP, FTP, SMTP, DNS, SNMP.

---

## Summary of Layer Roles

| **Layer**              | **Role**                           | **Example Protocols**         |
|------------------------|-----------------------------------|-------------------------------|
| **Application**        | User interaction & services      | HTTP, FTP, SMTP              |
| **Presentation**       | Data formatting & encryption     | SSL/TLS, JPEG                |
| **Session**            | Dialog management               | NetBIOS, RPC                 |
| **Transport**          | Reliable delivery & segmentation | TCP, UDP                     |
| **Network**            | Routing & logical addressing     | IP, ICMP                     |
| **Data Link**          | Framing & error handling         | Ethernet, Wi-Fi              |
| **Physical**           | Signal transmission              | Ethernet cables, fiber optics |

---

This layered approach allows for modularity, troubleshooting, and interoperability between different systems and technologies.
