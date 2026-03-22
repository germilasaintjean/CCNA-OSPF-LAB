## CCNA-OSPF-LAB  Multi‑Area OSPF Lab (Cisco Packet Tracer)
Built a multi‑area OSPF lab in Cisco Packet Tracer with four routers and two OSPF areas. Configured IP addressing, OSPF process 1, and verified neighbor adjacencies and routing using show ip ospf neighbor and show ip route. Tested end‑to‑end connectivity between hosts across multiple areas.

## 📁 **File Included**
- **OSPF multi-area lab.pkt** — Packet Tracer topology  

## 🌐 **Project Summary**

This project implements a multi‑router **multi‑area OSPF** network in Cisco Packet Tracer.  
The goal was to achieve full end‑to‑end connectivity between two PCs:

**PC1 → R1 → R2 → R3 → R4 → PC2**

<img width="975" height="248" alt="image" src="https://github.com/user-attachments/assets/5d125e64-b9d1-4530-95bd-37a553f53b06" />


Each router used a different subnet, and OSPF dynamically learned all routes.  
The final objective was for **PC1 to successfully ping PC2 (10.0.4.10)**.

### **Objectives**
- Configure correct IP addressing on all router interfaces  
- Ensure all interfaces were *up/up*  
- Assign correct OSPF areas (1 → 0 → 2)  
- Form OSPF neighbor relationships  
- Advertise all networks, including LANs  
- Verify routing tables and fix missing routes  
- Test connectivity hop‑by‑hop  

The final result was a fully functional multi‑area OSPF network.

---

## ⚠️ **Challenges Encountered and Solved**

### **1. PC1 connected to the wrong router interface**
- PC1 was plugged into R1 G0/1, but the gateway (10.0.1.1) was on G0/0.  
**Fix:** Corrected the interface/IP alignment.

---

### **2. R1 ↔ R2 link misconfigured**
- R1 could not ping 10.0.12.2 due to wrong ports, wrong IPs, shutdown interfaces, or cabling issues.  
**Fix:** Corrected IPs, ports, and ensured both interfaces were up/up.

---

### **3. Commands run in the wrong mode**
- Some commands were attempted in user mode (`>`).  
**Fix:** Used `enable` to enter privileged EXEC mode.

---

### **4. OSPF area mismatch between R2 and R3**
- Error seen:  
  `%OSPF-4-ERRRCV: Received invalid packet: mismatch area ID...`  
**Fix:** Placed the entire 10.0.23.0/24 link into **area 0** on both routers.

---

### **5. Incomplete OSPF neighbors**
- R2 had no neighbors due to area mismatch and link issues.  
**Fix:** Corrected OSPF network statements.

---

### **6. R1 missing route to 10.0.4.0/24**
- Caused:  
  `Reply from 10.0.1.1: Destination host unreachable.`  
**Fix:** Advertised R4’s LAN in OSPF.

---

### **7. R4’s LAN not advertised**
- R4 had IP 10.0.4.1 but no OSPF network statement.  
**Fix:** Added:  
  `network 10.0.4.0 0.0.0.255 area 2`

---

### **8. PC2 configuration verification**
- Ensured correct IP, mask, gateway, and cabling.

---

## 🎉 **Final Result**

- All OSPF neighbors formed correctly  
- All routes appeared in every router’s routing table  
- PC1 successfully pinged PC2 with **0% packet loss**  

The network converged fully and operated as designed.

---

## 🧰 **CLI Commands Used**

### **1. Basic Access**
```
enable
configure terminal
```

---

### **2. Interface Configuration**
```
interface GigabitEthernet0/x
ip address <IP> <MASK>
no shutdown
exit
```

---

### **3. OSPF Configuration**
```
router ospf 1
network <network> <wildcard> area <area>
no network <network> <wildcard> area <area>
```

---

### **4. Verification & Troubleshooting**
```
show ip interface brief
show ip route
show ip ospf neighbor
show run | section ospf
ping <IP>
```

---

## 🧩 **PC Configuration (Packet Tracer)**

Each PC was configured with:

- IP address  
- Subnet mask  
- Default gateway  

This ensured:

- PC1 could reach R1  
- PC2 could reach R4  
- End‑to‑end connectivity was possible  

